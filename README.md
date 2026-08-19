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
- 將票面与所用字体一并嵌入并导出高清 PNG
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

## 更新日志

### 2026-08-20

- 使用扩充版汇文明朝 WOFF2 字库，修复部分繁体字没有被字体覆盖的问题
- 同步更新网页预览与 PNG 导出的字体路径
- 字库验证包含 7,505 个映射字符
- 重新发布至 GitHub Pages

### 2026-08-19

- 将三份网页字体纳入仓库，解决上线后字体与本机预览不一致的问题
- 修复 PNG 导出时未完整嵌入票面字体的问题
- 接入 Supabase 匿名事件统计
- 新增车票生成与下载事件记录
- 增加匿名统计隐私提示
- 启用 GitHub Pages 自动部署

## 部署

GitHub Pages 从 `main` 分支根目录发布。合并到 `main` 后，GitHub Pages 会自动重新构建网站。

- 仓库：<https://github.com/Helen-224/taiwan-ticket-generator>
- 线上网站：<https://helen-224.github.io/taiwan-ticket-generator/>
