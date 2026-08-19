# 我的島嶼車票

一個以台灣老車票、復古印刷與島嶼手繪為靈感的紀念車票生成器。選擇出發日期、起點與終點後，即時產生專屬祝福車票，並可下載為 PNG 圖片。

[立即製作島嶼車票](https://helen-224.github.io/taiwan-ticket-generator/)

## 主要功能

- 選擇年、月、日，也支援過去日期
- 內建台灣特色站點與配對祝福
- 支援自訂起點、終點與祝福語
- 自訂內容會轉換為繁體中文顯示
- 自動匹配站點英文名稱
- 提供「島嶼手繪」與「纖維舊紙」票面風格
- 即時預覽日期、站點、方向、祝福語與 QR Code
- 將票面與所用字體一併嵌入並匯出高畫質 PNG
- 支援桌面與手機版面

## 使用方式

1. 選擇出發日期。
2. 選擇或自訂起點與終點。
3. 選擇票面風格。
4. 視需要輸入自訂祝福語。
5. 點擊「儲存我的車票」下載 PNG。

## 技術說明

本專案是可直接部署的靜態網站，主要由以下技術組成：

- HTML、CSS、原生 JavaScript
- SVG 即時票面渲染
- Canvas PNG 匯出
- 本地 WOFF2 網頁字體
- Supabase 匿名事件統計
- GitHub Pages 自動部署

## 字體

專案將票面所需字體放在 `assets/fonts/`，避免依賴使用者裝置字體：

- `HuiwenMingchao-GBK-subset.woff2`：纖維舊紙風格中文
- `Yomogi-Regular-common.woff2`：島嶼手繪風格
- `SpecialElite-Regular.woff2`：日期、英文站名與價格

PNG 匯出時會將對應字體轉為 Data URL 嵌入 SVG，降低線上預覽與下載圖片之間的字體差異。

## 匿名統計

為了解生成器的使用狀況，網站會向 Supabase 記錄匿名事件：

- 生成時間
- 起點與終點
- 票面風格
- 自動或自訂祝福語
- 是否點擊下載
- 匿名訪客 ID
- 裝置類型與來源頁面

不記錄姓名、聯絡方式或帳號資料。Supabase 的公開客戶端金鑰僅允許匿名新增事件，前端沒有讀取、修改或刪除資料的權限。

## 本地執行

這是純靜態網站，可直接開啟 `index.html`。若瀏覽器限制本地字體或資源載入，建議在專案目錄啟動本地伺服器：

```powershell
python -m http.server 8765
```

然後開啟 `http://127.0.0.1:8765/`。

## 專案結構

```text
.
├── assets/
│   └── fonts/
├── index.html
├── script.js
├── styles.css
└── README.md
```

## 更新日誌

### 2026-08-20

- 使用擴充版匯文明朝 WOFF2 字庫，修復部分繁體字未被字體覆蓋的問題
- 同步更新網頁預覽與 PNG 匯出的字體路徑
- 字庫驗證包含 7,505 個映射字元
- 將票面 QR Code 固定指向正式網站，掃碼即可再次製作車票
- 將 QR 生成程式納入本地資源，避免外部 CDN 失敗時產生無法掃描的圖案
- 增加標準四格留白區，提高手機掃碼成功率
- 讓 QR Code 底色跟隨兩種票紙風格，減少突兀色塊並保留掃碼對比度
- 重新發布至 GitHub Pages

### 2026-08-19

- 將三份網頁字體納入倉庫，解決上線後字體與本機預覽不一致的問題
- 修復 PNG 匯出時未完整嵌入票面字體的問題
- 接入 Supabase 匿名事件統計
- 新增車票生成與下載事件記錄
- 增加匿名統計隱私提示
- 啟用 GitHub Pages 自動部署

## 部署

GitHub Pages 從 `main` 分支根目錄發布。合併到 `main` 後，GitHub Pages 會自動重新建置網站。

- 倉庫：<https://github.com/Helen-224/taiwan-ticket-generator>
- 線上網站：<https://helen-224.github.io/taiwan-ticket-generator/>
