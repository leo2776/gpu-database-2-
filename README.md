🌐 前端語法與硬體資料庫（GPU / CPU / HTML / CSS / JS）

Web Language & Hardware Mega Dataset

本專案是一個大型、結構化的語法與硬體資料庫，內容包含：

✔ GPU 資料庫（gpu_py.json）

✔ CPU 資料庫（cpu.json）

✔ HTML 語法資料庫（html.json）

✔ CSS 語法資料庫（css.json）

✔ JavaScript 語法資料庫（js.json）

本專案中的所有資料皆以 JSON 格式 整理，方便：

AI 模型訓練

Parser / Linter 語法器

IDE / 語法補全系統

自製程式語言

教學、技術文件生成

硬體識別與性能分析工具

這是全中文且高擴充性的資料庫計畫，並持續更新中。

📁 專案結構
gpu-database-2/
│
├── cpu.json         # CPU 型號資料庫
├── css.json         # CSS 語法 / 屬性資料庫
├── gpu_py.json      # GPU 型號資料庫（含品牌、系列、分類）
├── html.json        # HTML 全元素語法資料庫（含過時元素）
├── js.json          # JavaScript 語法庫（關鍵字、運算子、型別等）
│
└── README.md        # 專案說明文件（本文件）

📌 CPU 資料庫（cpu.json）

內容包含：

Intel / AMD / Apple / ARM 各代 CPU

架構（Architecture）

執行緒數、核心數

代號（如：Skylake、Zen4）

適用設備（桌電 / 筆電 / 伺服器）

強度等級分類（可自定義）

用途：

本地硬體識別

AI 自動選擇運算策略

系統資源最佳化

📌 GPU 資料庫（gpu_py.json）

內容包含：

NVIDIA / AMD / Intel / Apple 全系列 GPU

桌機 / 筆電 / 伺服器 GPU

CUDA / ROCm / OpenCL 支援資訊

價位區間（可擴充）

低、中、高階分類

適合 AI 模型等級建議

用途：

AI 推理負載平衡（例如你之前說的「爆了也自動限制 50%」）

模型性能評估

自定義運算管理器

📌 HTML 資料庫（html.json）

內容包含：

所有 HTML 標籤（A~Z 全收錄）

每個標籤的屬性（attributes）

DOM interface

是否為 void element（如 <br>）

內容模型（Flow / Phrasing / Metadata…）

事件

過時元素（例如：<center>、<xmp>）

用途：

自製 HTML Parser

LSP / 語法補全

教學資料、AI 訓練集

📌 CSS 資料庫（css.json）

（目前為第一版，可逐步擴充）

內容包含：

常用 CSS 屬性

常用 CSS 單位

狀態、選擇器、顏色、函式

之後可加入完整 3000+ 屬性資料庫

用途：

自製 CSS Parser

網頁語法偵錯工具

AI 自動補全樣式

📌 JavaScript 資料庫（js.json）

內容包含：

JS 關鍵字（break、class、async、await…）

運算子（+、===、&&、?? 等）

基本型別

語句（if、for、switch…）

之後可加入整個 ECMAScript 語法樹

用途：

自製 JS 語法器

錯誤提示系統

程式碼自動生成器
我的網站:
ai:le2773ai.pages.dev
