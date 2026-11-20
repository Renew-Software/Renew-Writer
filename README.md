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

## Formatting
Bold (Ctrl+B), italic (Ctrl+I) and underline (Ctrl+U) are available from the toolbar and the keyboard.
- With nothing selected, a button only changes the text you type **from that point on**; text you already typed keeps its formatting. Turn a style on, type, then turn another on (or off) and carry on.
- With text selected, the button toggles that style on the selection only.
- Moving the caret picks up the formatting of the character before it, and the toolbar buttons show what is active.
- The font menu works the same way: with nothing selected it sets the font for text you type from now on (earlier text keeps its font); with text selected it changes just that text. The menu shows the font at the caret.
- The size menu (in points) works the same way: with nothing selected it sets the size for text you type from now on; with text selected it changes just that text. The default is 10.5pt. Each line is as tall as the biggest character on it, so a line of small text stays tight and a line with one large word grows to fit it.
- Formatting is saved to and loaded from `.docx` and `.odt` including the font and size (direct run formatting only; `.txt` is plain text).
- Exports match the editor: the same page size, 0.5 inch margins, line spacing and kerning, so text wraps the same way in Word or LibreOffice Writer as it does on screen (a page break can land one line apart, as Word and Writer space the top of a paragraph slightly differently).
- Undo/redo: Ctrl+Z / Ctrl+Y (or Ctrl+Shift+Z).

## Fonts
The font menu only lists fonts that are installed on the computer, and all of them are free/open-source. To get a wide selection on Ubuntu/Debian:
```bash
sudo apt install -y fonts-liberation fonts-crosextra-carlito fonts-crosextra-caladea fonts-dejavu fonts-noto-core fonts-noto-mono fonts-open-sans fonts-roboto fonts-lato fonts-inter fonts-cantarell fonts-hack fonts-firacode fonts-ibm-plex fonts-jetbrains-mono fonts-lora fonts-ebgaramond
```
Package names can differ slightly between releases. Restart R-Writer after installing fonts.
