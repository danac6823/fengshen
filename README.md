# 心中有豐盛，豐盛自來 — 離線版 PWA

單檔離線記帳 App。資料存在「這台裝置的瀏覽器」(localStorage)，不會上傳雲端。

## 檔案
- index.html（整個 App，含全部功能）
- manifest.json（App 名稱／圖示設定）
- sw.js（離線快取）
- icon-192.png / icon-512.png / icon-180.png（圖示）

## 怎麼用（最簡單：Netlify Drop）
1. 把整個 sanfen-pwa 資料夾下載到電腦。
2. 開 https://app.netlify.com/drop ，把整個資料夾「拖進去」。
3. 它會給你一個網址（https://xxxx.netlify.app）。
4. 手機開那個網址 → 瀏覽器選單 →「加入主畫面」。
5. 之後從主畫面圖示開啟，就是全螢幕 App，可離線使用。

## 注意
- Service Worker 需要 https 才會啟用（Netlify 自帶 https）。直接用 file:// 打開只能測畫面，無法安裝/離線。
- 第一次開啟需連線下載元件（React 等），之後會被快取，可離線。
- 資料只在「這台裝置」。換手機或清除瀏覽器資料會不見。要搬移／備份請用 App 內的「匯出 JSON」，到新裝置再「匯入 JSON」。
- 更新版本：重新部署後，App 會在下次連線時自動更新（sw.js 的 CACHE 版本是 fengsheng-v1，改版時請更新版號）。


## 改版（更新 App）怎麼做
1. 用新版的整個資料夾，重新上傳／覆蓋到原本的站台（Netlify 拖一次、或 GitHub 重新 commit）。
2. **重點**：打開 `sw.js`，把第二行的版號 `fengsheng-v1` 數字 +1（例如改成 `fengsheng-v2`），存檔再上傳。
   - 這一步會讓舊快取失效，使用者下次連線時自動換成新版。不改版號的話，可能會一直看到舊版。

## 用 GitHub Pages（網址固定、適合長期維護）
1. 到 github.com 註冊帳號並登入。
2. 右上「＋」→ New repository，名稱例如 `fengsheng`，選 **Public**，建立。
3. 進入該 repo →「Add file → Upload files」→ 把這個資料夾**裡面的所有檔案**（index.html、manifest.json、sw.js、三個 icon）拖進去 → Commit。
   - 注意：`index.html` 要在 repo 的「根目錄」（不要再包一層資料夾）。
4. repo 上方 **Settings → Pages** → Source 選「Deploy from a branch」→ Branch 選 `main` / `/ (root)` → Save。
5. 等 1～2 分鐘，網址會是 `https://你的帳號.github.io/fengsheng/`。
6. 手機開這個網址 →「加入主畫面」即可。（本 App 用相對路徑，放在子目錄也能正常運作。）
7. 之後要改版：重新上傳 index.html（並把 sw.js 版號 +1）→ Commit，幾分鐘後自動更新 。
