import { useEffect } from 'react';

const useReloadWarning = () => {
  useEffect(() => {
    let isReloading = false;

    // Detect user pressing reload keys
    const markReload = (e: KeyboardEvent) => {
      if (e.key === 'F5' || (e.ctrlKey && e.key.toLowerCase() === 'r')) {
        sessionStorage.setItem('isReloading', 'true');
      }
    };

    // Detect browser refresh button (visibilitychange fires before unload)
    const markReloadOnVisibilityChange = () => {
      if (document.visibilityState === 'hidden') {
        const navEntries = performance.getEntriesByType("navigation") as PerformanceNavigationTiming[];
        const navType = navEntries[0]?.type;
        if (navType === "reload") {
          sessionStorage.setItem('isReloading', 'true');
        }
      }
    };

    const handleBeforeUnload = (e: BeforeUnloadEvent) => {
      const reloadingFlag = sessionStorage.getItem('isReloading');

      if (reloadingFlag === 'true') {
        // User is reloading -> skip alert
        sessionStorage.removeItem('isReloading');
        return;
      }

      // Normal tab close or navigation away
      e.preventDefault();
      e.returnValue = ''; // For compatibility
    };

    const handleUnload = () => {
      const reloadingFlag = sessionStorage.getItem('isReloading');

      if (reloadingFlag === 'true') {
        // Skip DB deletion on reload
        sessionStorage.removeItem('isReloading');
        return;
      }

      console.log('Deleting IndexedDB (user leaving page)');

      try {
        const req = indexedDB.deleteDatabase('ecc-files-db');
        req.onerror = () => console.error('Error deleting IndexedDB');
      } catch (err) {
        console.error('Failed deleting IndexedDB:', err);
      }
    };

    // Listeners
    window.addEventListener('beforeunload', handleBeforeUnload);
    window.addEventListener('unload', handleUnload);
    window.addEventListener('keydown', markReload);
    document.addEventListener('visibilitychange', markReloadOnVisibilityChange);

    return () => {
      window.removeEventListener('beforeunload', handleBeforeUnload);
      window.removeEventListener('unload', handleUnload);
      window.removeEventListener('keydown', markReload);
      document.removeEventListener('visibilitychange', markReloadOnVisibilityChange);
    };
  }, []);
};

export default useReloadWarning;

