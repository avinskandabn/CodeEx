function extractFiles(obj: any, result: any[] = []) {
  if (!obj || typeof obj !== "object") return result;

  // If this object has a "files" array → process it
  if (Array.isArray(obj.files)) {
    obj.files.forEach((file) => {
      if (file.name && file.fileComplexityCount) {
        result.push({
          name: file.name,
          fileComplexityCount: file.fileComplexityCount,
        });
      }
      // A file can itself have nested "files"
      extractFiles(file, result);
    });
  }

  // Recursively check all keys of the current object
  for (const key in obj) {
    if (typeof obj[key] === "object") {
      extractFiles(obj[key], result);
    }
  }

  return result;
}
