# 🔄 Single File Converter - Offline Media & Text Converter

A powerful, 100% offline HTML file converter that works without an internet connection or HTTP server. Simply open the HTML file in your browser and start converting!

## ✨ Features

- **100% Offline** - No internet connection required
- **No Server Needed** - Works under `file://` protocol
- **Self-Contained** - Everything in a single HTML file
- **Multiple Format Support** - Video, audio, images, and text files
- **Drag & Drop Interface** - Easy to use
- **Real-time Preview** - See your converted files before downloading
- **Quality Control** - Adjust output quality and bitrates

## 🚀 Quick Start

1. Download `converter.html` to your computer
2. Double-click the file to open it in your web browser
3. Drag and drop a file or click to select one
4. Choose your desired output format
5. Click "Convert File"
6. Download your converted file!

**That's it!** No installation, no setup, no internet needed.

## 📋 Supported Formats

### 🎥 Video Conversion
- **Supported Inputs:** MP4, WebM, AVI, MOV, MKV, FLV, WMV, OGV
- **Output Formats:** MP4, WebM
- **Features:** Adjustable video/audio bitrate, preserves quality

### 🎵 Audio Conversion
- **Supported Inputs:** MP3, WAV, OGG, AAC, FLAC, M4A, WMA, OPUS
- **Output Formats:** MP3, WAV, OGG
- **Features:** Bitrate control, high-quality conversion

### 🖼️ Image Conversion
- **Supported Inputs:** PNG, JPG, JPEG, GIF, BMP, WebP, SVG, ICO
- **Output Formats:** PNG, JPEG, WebP
- **Features:** Quality slider (0.1 - 1.0), maintains dimensions

### 📝 Text Format Conversion
- **Supported Inputs:** TXT, JSON, CSV, HTML, XML, MD, LOG
- **Output Formats:** TXT, JSON, CSV, HTML, Base64
- **Special Features:**
  - CSV ↔ JSON conversion
  - HTML ↔ TXT conversion
  - Base64 encode/decode
  - Format preservation

## 🔧 How It Works

This converter uses browser-native APIs to perform all conversions locally:

- **Canvas API** - For image and video frame processing
- **MediaRecorder API** - For video/audio encoding
- **Web Audio API** - For audio processing and format conversion
- **FileReader API** - For text file processing
- **Blob API** - For file creation and downloads

All processing happens in your browser's memory - nothing is uploaded or sent anywhere!

## 💡 Usage Tips

### Image Conversion
- Use the **Quality slider** to balance between file size and image quality
- Quality of 0.9 provides excellent quality with good compression
- WebP format offers the best compression

### Audio Conversion
- Default bitrate of 128 kbps is suitable for most uses
- For music, consider 256-320 kbps for better quality
- WAV format is lossless but creates larger files

### Video Conversion
- Video bitrate of 2500 kbps is a good balance for HD content
- WebM format typically produces smaller files than MP4
- Processing may take time for large videos

### Text Conversion
- CSV to JSON conversion assumes first row contains headers
- JSON to CSV requires an array of objects
- Base64 encoding is useful for embedding data in code

## 🌐 Browser Compatibility

Works in all modern browsers:
- ✅ Chrome/Edge (Recommended)
- ✅ Firefox
- ✅ Safari
- ✅ Opera

**Note:** Some format combinations may have limited support depending on your browser's codec support.

## 🔒 Privacy & Security

- **100% Private** - All conversions happen locally in your browser
- **No Data Collection** - Nothing is stored or transmitted
- **No External Dependencies** - No CDNs, no external scripts
- **Works Offline** - Disconnect your internet and it still works!

## ⚡ Performance Notes

- Large video files (>100MB) may take several minutes to convert
- Your computer's CPU/GPU capabilities affect conversion speed
- For best performance, close unnecessary browser tabs
- Mobile devices may struggle with large video files

## 📦 Technical Details

- **File Size:** Single HTML file (~30KB)
- **Dependencies:** None - completely self-contained
- **Internet Required:** No
- **Server Required:** No
- **Installation Required:** No

## 🐛 Troubleshooting

**"Conversion failed" error:**
- Make sure your browser supports the input/output formats
- Try a different output format
- Check that the file isn't corrupted

**Video conversion is slow:**
- This is normal for large files
- The browser is processing every frame
- Be patient - it will complete

**Some formats don't appear:**
- Your browser may not support certain codecs
- Try using Chrome/Edge for best compatibility

**File won't open in browser:**
- Make sure it's saved as `.html`
- Try right-click → "Open with" → Browser

## 🤝 Contributing

This is an open-source project. Feel free to:
- Report bugs or issues
- Suggest new features
- Improve the code
- Add more format support

## 📄 License

This project is open source and available for anyone to use, modify, and distribute.

## 🎯 Use Cases

- Convert videos for different platforms
- Extract audio from video files
- Convert images for web optimization
- Transform data between CSV and JSON
- Encode/decode Base64 data
- Quick format conversions without online tools
- Work offline in areas without internet
- Process sensitive files without uploading them

---

**Enjoy your offline converting!** 🎉

No internet. No server. Just pure browser magic. ✨
