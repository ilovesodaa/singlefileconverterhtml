# Single File Converter

## Project Overview
A single-file HTML media and text converter powered by FFmpeg.wasm. The entire application lives in `converter.html` — no build system, no separate JS/CSS files, no server required.

## Architecture
- **One file**: `converter.html` contains all HTML, CSS, and JavaScript
- **FFmpeg.wasm v0.11.6**: Loaded via `<script src>` from jsdelivr CDN (classic script tag, NOT ES modules)
- **FFmpeg core v0.11.0**: WASM binary loaded at runtime from CDN
- **No HTTP server needed**: Must work when opened directly as a `file://` in the browser

## Key Constraints
- **Single HTML file only** — never split into separate files
- **No ES modules** — `<script type="module">` and `import` statements break `file://` protocol. Use classic `<script>` tags only
- **No build tools** — no npm, webpack, vite, etc.
- **CDN dependencies only** — external libs loaded via `<script src="https://cdn.jsdelivr.net/...">`
- **Text conversions don't use FFmpeg** — they use plain JS string manipulation

## FFmpeg.wasm API (v0.11.6)
This project uses the v0.11.x API, NOT v0.12.x:
```js
const { createFFmpeg, fetchFile } = FFmpeg;   // Global FFmpeg object from CDN script
const ffmpeg = createFFmpeg({ corePath: '...', progress: ({ ratio }) => {} });
await ffmpeg.load();
ffmpeg.FS('writeFile', name, await fetchFile(file));  // Write to virtual FS
await ffmpeg.run('-i', 'input.mp4', 'output.webm');   // Run conversion
const data = ffmpeg.FS('readFile', 'output.webm');     // Read from virtual FS
ffmpeg.FS('unlink', name);                             // Cleanup virtual FS
```

## Conversion Types
- **Video**: FFmpeg transcode (MP4, WebM, AVI, MOV, MKV, GIF, etc.)
- **Audio**: FFmpeg transcode (MP3, WAV, OGG, AAC, FLAC, M4A, Opus)
- **Image**: FFmpeg conversion (PNG, JPEG, WebP, BMP, GIF, TIFF)
- **Video-to-Audio**: FFmpeg with `-vn` flag
- **Audio-to-Video**: FFmpeg `lavfi` color input + audio mux
- **Text**: Pure JS (CSV/JSON/HTML/TXT/Base64) — no FFmpeg involved

## Shared Helper
`runFFmpegConversion(file, outputFormat, buildArgs, mimeType)` handles the full lifecycle: init check, writeFile, run, readFile, cleanup, progress, error handling. Each conversion function is a thin wrapper that builds FFmpeg args.
