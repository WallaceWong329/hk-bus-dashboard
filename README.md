**# hk-bus-dashboard**# 🚌 香港巴士實時到站儀表板 (HK Bus ETA Dashboard)

這是一個輕量級、零依賴的單頁網頁應用程式 (SPA)，專為顯示香港巴士實時到站時間 (ETA) 而設。本專案特別針對**舊款裝置（例如運行 iOS 9 的 iPad 2）**進行了深度優化，非常適合作為家中的「掛牆式智能顯示器」。介面採用全螢幕鎖定設計，禁止上下滑動，完美切分螢幕空間。

## ✨ 核心功能

* **完美兼容舊世代裝置：** 全面採用純原生 JavaScript (Vanilla JS / ES5) 及傳統的 `XMLHttpRequest` 寫成。完全不依賴 React、Vue 等現代框架，確保在舊版瀏覽器（如 iOS 9 的 Safari）上也能極速、穩定地運作。
* **聯營路線雙重融合 (Joint-Operated Route Fusion)：** 智能處理聯營過海路線（如 118 號線）。系統會同時向九巴及城巴的伺服器發送請求，自動過濾重疊的班次，並將兩巴的到站時間混合，按時間先後排序。介面上更會附以搶眼的顏色標籤（九巴為紅色、城巴為黃色）以資識別。
* **無分方向智能搜尋：** 針對九巴與城巴對於「去程 (Outbound) / 回程 (Inbound)」定義相反的痛點，實作了雙向地毯式搜尋，確保一定能準確抓出對應的車站 ID，防止系統卡死。
* **智能防走位排版：** 使用 CSS Flexbox 構建嚴格的 2x2 網格佈局。當某條路線的到站班次少於 3 班時，底層代碼會自動補上「透明的隱藏空行」來撐住原本的空間，防止排版出現尷尬的移位或空白。
* **自動更新與快取機制 (Caching)：** 會將搜尋到的巴士站 ID 寫入瀏覽器的 Local Storage 進行快取，大幅減少每次重新載入時的 API 請求負擔，並設有每 30 秒自動刷新到站時間的功能。

## 🚀 如何使用

由於這是一個純前端的網頁，不需要安裝任何後端伺服器（Node.js/Python 等）即可直接執行：

1. 下載或 Clone 此儲存庫 (Repository)。
2. 直接使用任何網頁瀏覽器打開 `bus.html` 檔案即可看到畫面。
3. *強烈建議：* 將代碼上傳至 GitHub 後，開啟 **GitHub Pages** 功能進行免費網頁託管，這樣你就可以在 iPad 上輸入一串簡單的網址直接觀看。

## 🛠 路線設定與更改

你可以透過修改 `bus.html` 代碼內的 `routeConfigs` 物件，來輕鬆更改你想追蹤的巴士路線與車站：

```javascript
var routeConfigs = {
    '8P':  { searchKeyword: '樂軒臺', stopId: null },
    '118': { searchKeyword: '樂軒臺', stopId: null, kmbStopId: null }, // 聯營路線專用的雙 ID 設定
    '788': { searchKeyword: '翠灣',   stopId: null },
    '789': { searchKeyword: '翠灣',   stopId: null }
};
