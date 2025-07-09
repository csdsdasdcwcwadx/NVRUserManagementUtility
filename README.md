NVR 使用者管理工具（NVR User Management Utility）

## 專案簡介
本工具是一款輕量化的使用者管理介面，主要用於管理不同 NVR（網路影像錄影機）來源的使用者與群組資料，支援新增、刪除使用者與群組，以及變更密碼等操作。

## 專案目的
 - 由於 WPF 桌面應用的限制，本專案採用 React.js 製作前端，打包後嵌入 WPF 框架中，整體採 `file://` 路徑運行，因此所有 HTTP 請求皆需透過 WPF 的介面進行轉送，並透過 `window.chrome.webview.postMessage` 實現與前端的溝通。
 - 產品用於針對多台的NVR Source 進行同步操作。

## 功能特色
- 管理多個 NVR 的使用者與群組資料
- 支援新增 / 刪除使用者、使用者群組
- 支援密碼編碼 / 解碼與變更
- 自動偵測區域網路內的 Domain 使用者帳號，供選擇登入
- 根據不同 API Response 執行錯誤處理與提示訊息
- XML 資料解析，並支援排序與過濾功能

## 使用技術
- **前端框架**：React.js（Webpack 打包至 WPF）
- **桌面應用**：WPF (.NET)
- **資料傳輸介面**：`window.chrome.webview.postMessage` / `addEventListener('message')`
- **狀態管理**：Redux
- **資料處理**：XML 字串解析、自定錯誤處理類別（CustomError）
- **使用者清單載入**：根據區域網路 Domain 動態載入帳號清單

## 介面截圖

### 主介面（Dashboard）
![image](https://github.com/user-attachments/assets/0922b1e3-dff8-4403-a463-6b0fe8028aa0)

### 使用者管理
![image](https://github.com/user-attachments/assets/36e6a607-5ba1-4eb6-8f4f-1ea0eeed2114)

### 區網使用者偵測
![image](https://github.com/user-attachments/assets/67f1270e-9dc4-44e8-a5ea-6a03047d8f5e)

## 專案挑戰與解決方式
 - **跨平台通信問題**：因無法使用原生 HTTP，改以 postMessage 傳送與接收 API 資料，並建構完整錯誤處理流程。
 - **資料格式多樣性**：NVR 回傳資料多為 XML，需設計穩定的解析流程與錯誤碼擷取邏輯。
 - **動態更新資料狀態**：透過 Redux 管理各項操作緩衝區（buffer），並在操作完成或失敗後清除資料。
