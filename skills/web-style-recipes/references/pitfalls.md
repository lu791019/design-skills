# 共通技術陷阱與對策

交付前逐條對照。風格專屬陷阱寫在各風格檔。

| # | 陷阱 | 症狀 | 對策 |
|---|---|---|---|
| 1 | **鏡頭／麥克風只在安全來源可用** | 雙擊打開 HTML，`getUserMedia` 直接失敗或 `navigator.mediaDevices` 是 undefined | 只在 `localhost` 或 HTTPS 才能用。本機一律 `npx serve .` 後開 `http://localhost:3000`；部署走 HTTPS |
| 2 | **file:// 時 Canvas 讀不到本機圖片像素** | `getImageData` 丟 SecurityError（canvas 被污染），去背 PNG 反推亮度失敗 | 用本機伺服器開；或把小圖轉 base64 內嵌（`data:` URL 不會污染 canvas）；外部圖加 `crossOrigin="anonymous"` 且伺服器要回 CORS 標頭 |
| 3 | **全螢幕逐像素模擬太慢** | 熱擴散、流體、粒子場掉到個位數 FPS | 在低解析網格（約 200–300 欄）算，畫到小 canvas 再用 CSS 放大（`image-rendering` 視風格選 pixelated 或平滑）；每幀避免配置新陣列，雙緩衝交換 |
| 4 | **沒顧到減少動態偏好** | 前庭敏感使用者頭暈；無障礙稽核扣分 | 讀 `matchMedia('(prefers-reduced-motion: reduce)')` 並監聽變化：停自動旋轉／捲動，改成靜態畫面＋使用者觸發才動；保留一顆頁內「動態開／關」按鈕 |
| 5 | **只綁滑鼠事件** | 手機點了沒反應、拖曳時整頁跟著捲 | 一律用 Pointer Events（`pointerdown/move/up`）＋ `setPointerCapture`；可拖曳區設 `touch-action: none` |
| 6 | **100vh 單屏在手機被網址列吃掉** | 底部工具列或按鈕被切掉、出現多餘捲動 | 用 `100dvh`（後備 `100vh`），或 JS 以 `innerHeight` 設 `--vh`；`body` 設 `overflow: hidden` 時確認內容真的塞得下 |
| 7 | **手機跑桌機的特效量** | 發燙、掉幀、電量狂掉 | 依 `matchMedia('(pointer: coarse)')` 或螢幕寬度降粒子數（約桌機的 1/3）、拿掉大半徑 `filter: blur` 與 `backdrop-filter`；限制 `devicePixelRatio` 上限 2；分頁隱藏時（`visibilitychange`）暫停迴圈 |
| 8 | **權限被拒就整頁壞掉** | 使用者按「封鎖」後一片黑或卡在等待 | 先展示不需權限的示範模式，再由按鈕請求權限；被拒（`NotAllowedError`）、無裝置（`NotFoundError`）、非安全來源分別給頁內說明與「改用示範／上傳」的替代路徑，不用 `alert` |
| 9 | **localStorage 讀寫沒包 try/catch** | 無痕模式、儲存已滿、或被封鎖時整支 JS 中斷 | 讀寫都包 try/catch；讀到壞 JSON 時回預設值；寫入失敗時頁面照常運作並低調提示「這次不會保存」 |
| 10 | **開頁一片空白** | 要等使用者授權或上傳才有畫面，第一印象是「壞了」 | 開頁就有內容：示範訊號、預設圖、模擬目標。**模擬內容要標示**（例如角落小字「DEMO／模擬訊號」），避免使用者誤以為是真資料或真鏡頭 |

## 交付前自查（最短版）

- [ ] 用 `npx serve` 開過，不是雙擊檔案
- [ ] 桌機 1440 寬、手機 390 寬各看一次
- [ ] 開啟系統「減少動態效果」再看一次
- [ ] 拒絕一次權限，確認有頁內提示與替代路徑
- [ ] 手機能用手指完成一句話流程的每一步
- [ ] Console 無錯誤
