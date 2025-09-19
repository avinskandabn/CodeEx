import React, { useState } from "react";

const FileUploadTable: React.FC = () => {
  const [currentSelectedFiles, setCurrentSelectedFiles] = useState<File[]>([]);

  // Handle adding new files
  const handleFileChange = (event: React.ChangeEvent<HTMLInputElement>) => {
    if (event.target.files) {
      const newFiles = Array.from(event.target.files);
      setCurrentSelectedFiles((prev) => [...prev, ...newFiles]);
    }
  };

  // Handle removing a file
  const handleRemove = (fileName: string) => {
    setCurrentSelectedFiles((prev) =>
      prev.filter((file) => file.name !== fileName)
    );
  };

  return (
    <div>
      <input type="file" multiple onChange={handleFileChange} />

      <table border={1} style={{ marginTop: "10px", width: "100%" }}>
        <thead>
          <tr>
            <th>Files/folder path</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          {currentSelectedFiles.map((file, index) => (
            <tr key={`${file.name}-${index}`}>
              <td>{file.name}</td>
              <td>
                <button onClick={() => handleRemove(file.name)}>Remove</button>
              </td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};

export default FileUploadTable;
