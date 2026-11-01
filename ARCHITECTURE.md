# Inventra AI — deployment and on-device AI architecture

## Hosting boundary

- **GitHub repository:** source code, static site, model integration code, and deployment workflows.
- **GitHub Pages:** serves the static HTML/CSS/JavaScript app over HTTPS. It cannot execute Python, store private business records, or run a shared database.
- **Phone/browser:** runs camera capture, barcode recognition, future visual AI inference, and offline inventory storage. No laptop server is required.
- **Optional cloud sync:** a separate free-tier backend (for example Supabase) is required for secure multi-device accounts and shared inventory. GitHub itself is **not** the database.

## Local AI requirement

Vision inference must execute **on the user's device**, not on a remote AI API or a laptop acting as a server. Preferred approach:

1. Use native BarcodeDetector when available (already implemented).
2. Load a compatible, appropriately licensed browser vision model using Transformers.js / ONNX Runtime Web and WebGPU where supported; provide a CPU/WASM fallback if feasible.
3. Download model weights on first use and cache them for subsequent sessions; make download size, device support, storage needs and offline availability explicit.
4. Process camera frames on-device. Recognized labels are suggestions, not guaranteed product IDs or exact counts.
5. Prompt for name, variant and quantity when confidence is insufficient or packaging is opaque. Never infer contents of a sealed box.
6. Keep confirmation vs autonomous modes, but avoid repeatedly adding the same item across consecutive frames.

**Current status:** the existing site implements barcode scanning and manual entry only. A visual AI model has **not** yet been integrated or benchmarked. Do not describe the scanner as visual AI until that work is complete.

## Offline and synchronization

The existing prototype uses localStorage and can lose data if browser storage is cleared. The next implementation should migrate to IndexedDB, add a service worker for offline app assets, and queue immutable inventory operations with unique IDs. Once online, synchronize operations to an authenticated cloud database with business-scoped access controls and idempotent writes. A free tier has usage and availability limits.

## Deployment

Enable GitHub Pages: Settings → Pages → Deploy from a branch → main → /(root). URL: https://djamiechen.github.io/Inventra-AI/

## Important privacy and licensing requirements

Camera frames should remain on-device for recognition unless a user explicitly opts into upload. Check the model weights' license, browser support and mobile memory requirements before shipping. Do not place cloud service secrets in the public GitHub repository.
