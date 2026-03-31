# Single File Converter

## Project Overview
A single-file HTML media and text converter powered by FFmpeg.wasm. The entire application lives in `converter.html` — no build system, no separate JS/CSS files, no server required.

## Architecture
- **One file**: `converter.html` contains all HTML, CSS, and JavaScript
- **FFmpeg.wasm v0.12.15**: Loaded via `<script src>` UMD builds from jsdelivr CDN (classic script tags, NOT ES modules)
- **FFmpeg util v0.12.2**: Provides `toBlobURL` and `fetchFile` helpers (UMD build)
- **FFmpeg core v0.12.10**: WASM binary fetched from CDN and converted to blob URL via `toBlobURL`
- **No HTTP server needed**: Must work when opened directly as a `file://` in the browser

## Key Constraints
- **Single HTML file only** — never split into separate files
- **No ES modules** — `<script type="module">` and `import` statements break `file://` protocol. Use classic `<script>` tags only
- **No build tools** — no npm, webpack, vite, etc.
- **CDN dependencies only** — external libs loaded via `<script src="https://cdn.jsdelivr.net/...">`
- **WASM loaded as blob URL** — `toBlobURL` fetches the WASM binary from CDN and converts it to a blob URL for `file://` compatibility
- **Text conversions don't use FFmpeg** — they use plain JS string manipulation

## FFmpeg.wasm API (v0.12.x UMD)
This project uses v0.12.x UMD builds. Globals: `FFmpegWASM` and `FFmpegUtil`.
```js
// Load via UMD script tags (NOT ES modules)
// <script src="https://cdn.jsdelivr.net/npm/@ffmpeg/ffmpeg@0.12.15/dist/umd/ffmpeg.js"></script>
// <script src="https://cdn.jsdelivr.net/npm/@ffmpeg/util@0.12.2/dist/umd/index.js"></script>

var ffmpeg = new FFmpegWASM.FFmpeg();
var baseURL = 'https://cdn.jsdelivr.net/npm/@ffmpeg/core@0.12.10/dist/umd';
await ffmpeg.load({
    coreURL: await FFmpegUtil.toBlobURL(baseURL + '/ffmpeg-core.js', 'text/javascript'),
    wasmURL: await FFmpegUtil.toBlobURL(baseURL + '/ffmpeg-core.wasm', 'application/wasm'),
});
await ffmpeg.writeFile('input.mp4', await FFmpegUtil.fetchFile(file));
await ffmpeg.exec(['-i', 'input.mp4', 'output.webm']);
var data = await ffmpeg.readFile('output.webm');
await ffmpeg.deleteFile('input.mp4');
await ffmpeg.deleteFile('output.webm');
```

## Conversion Types
- **Video**: FFmpeg transcode (MP4, WebM, AVI, MOV, MKV, GIF, etc.)
- **Audio**: FFmpeg transcode (MP3, WAV, OGG, AAC, FLAC, M4A, Opus)
- **Image**: FFmpeg conversion (PNG, JPEG, WebP, BMP, GIF, TIFF)
- **Video-to-Audio**: FFmpeg with `-vn` flag
- **Audio-to-Video**: FFmpeg `lavfi` color input + audio mux
- **Text**: Pure JS (CSV/JSON/HTML/TXT/Base64) — no FFmpeg involved

## Shared Helper
`runFFmpegConversion(file, outputFormat, buildArgs, mimeType)` handles the full lifecycle: init check, writeFile, exec, readFile, cleanup, progress, error handling. Each conversion function is a thin wrapper that builds FFmpeg args.
