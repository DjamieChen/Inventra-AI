# Inventra AI

Offline-first mobile inventory registration prototype.

## Try it

The website is a static `index.html` that can be hosted on GitHub Pages. In repository **Settings → Pages**, select **Deploy from a branch**, branch **main**, folder **/(root)**, and save. After deployment completes, open:

https://djamiechen.github.io/Inventra-AI/

## Current features

- Manual product registration, with optional SKU/barcode, brand, and variant
- Exact barcode/SKU matching or normalized name + brand + variant matching
- Confirm-before-add mode and automatic registration for known barcode matches
- Device-local inventory and transaction history (localStorage)
- Quantity adjustments, CSV import and export
- Camera barcode scanning in browsers supporting BarcodeDetector and getUserMedia

## Important limitations

This is an early functional prototype, **not a deployed multi-user inventory service**. Data is only stored on the device/browser that created it; clearing browser data deletes it. Export CSV backups regularly. Import adds quantities, rather than replacing the database. There is no authentication, shared cloud storage, offline service worker, product image recognition, or server synchronization yet. BarcodeDetector support varies by browser. Scanning requires HTTPS or localhost. The camera only detects barcodes, not unlabeled products or box contents.

The Python backend from the separate prototype has not yet been ported into this repository. Future phases will include IndexedDB, an installable PWA, cloud sync, authentication/roles, and on-device computer vision.

## Cost

No paid APIs are required for this prototype. GitHub Pages is free for public repositories subject to GitHub usage policies.
