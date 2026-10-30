# 📌 Pin Saver — Pinterest Image & Video Downloader

A lightweight Chrome / Edge / Brave extension (Manifest V3). Open any Pinterest pin and a **Download** button appears right below the image or video — one click and the file is saved in original quality.

> ⚠️ Independent project. Not affiliated with Pinterest. For personal use only — respect the creators' rights and Pinterest's Terms of Service.

## ✨ Features
- Download button shown **below the pin's image/video** (works with Pinterest's single-page navigation)
- **Images**: tries the `originals` quality first, then falls back to smaller sizes
- **Videos**: finds a direct MP4 via multiple sources; if only an HLS (`.m3u8`) stream exists, it downloads the segments and **converts them to MP4 in the browser**
- Progress shown on the button (`Downloading 45%`)
- Popup with live status, download counter and developer details
- No tracking, no external servers, no analytics

## 📥 Installation (from source)
1. Download the latest ZIP from the [Releases](../../releases) page (or `git clone` this repo)
2. Extract it
3. Open `chrome://extensions` (Edge: `edge://extensions`)
4. Turn on **Developer mode**
5. Click **Load unpacked** and select the extracted folder
6. Pin the extension to the toolbar (puzzle icon → pin)

## 🚀 Usage
1. Open any pin on Pinterest (`/pin/...`)
2. Click the red **Download Image / Download Video** button under the media
3. Files are saved to `Downloads/Pinterest/`

## 🧠 How it works
| Part | File | Job |
|---|---|---|
| Content script | `content.js` | Detects pin pages (SPA), finds the main media, places the button, collects URLs |
| HLS converter | `hls.js` + `mux.js` | Downloads HLS segments and remuxes MPEG-TS → MP4 |
| Service worker | `background.js` | Tries candidate URLs one by one via `chrome.downloads`, keeps the counter |
| Popup | `popup.html/css/js`, `config.js` | Status, how-to, counter, developer card |

## 🔒 Permissions
| Permission | Why |
|---|---|
| `downloads` | Save files to disk |
| `storage` | Local download counter |
| `activeTab` | Show status of the current tab in the popup |
| Host access to `pinterest.*` and `pinimg.com` | Read the pin and fetch the media |

All data stays on your device.

## 🛠️ Customize the developer card
Edit [`config.js`](config.js), then reload the extension.

## 🐞 Troubleshooting
- **Button not showing** → refresh the Pinterest tab after installing/updating
- **Video fails** → open DevTools (`F12`) → Console, copy the `[PinSaver] video sources:` line and attach it to a [new issue](../../issues)
- Pinterest changes its site often — selectors/APIs may need updates

## 🤝 Contributing
Issues and pull requests are welcome.

## 📄 License
[MIT](LICENSE). Bundled third-party code: see [NOTICE.md](NOTICE.md) (mux.js, Apache-2.0).
