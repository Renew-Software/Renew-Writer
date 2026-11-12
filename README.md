# R-Writer (Rust + Tauri)

A lightweight, native, paginated desktop word processor built in **Rust** with **Tauri v2**, supporting `.docx`, `.odt`, and `.txt` files.

## Project Structure
- `src-tauri/` — Native Rust backend, Tauri v2 configuration, and `.deb` bundler settings
- `ui/` — Frontend document editor (`index.html` + `jszip.min.js`)
- `.github/workflows/build-deb.yml` — Automated GitHub Actions CI that compiles the Rust binary and packages it into a `.deb` installer

## Building Locally (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install -y libwebkit2gtk-4.1-dev build-essential curl wget file libxdo-dev libssl-dev libayatana-appindicator3-dev librsvg2-dev
curl -sL https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js -o ui/jszip.min.js
cargo install tauri-cli --version "^2.0.0"
cargo tauri build --bundles deb
```
The compiled `.deb` will be generated at:
`src-tauri/target/release/bundle/deb/R-Writer_1.0.0_amd64.deb`
