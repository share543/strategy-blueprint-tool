# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [2.0.0] - 2026-10-04

### Fixed（經三層實測確認）

- **XSS 漏洞**：使用者輸入直接進 `innerHTML`，`<img src=x onerror=...>` 會被執行。
  新增 `esc()` / `num()` / `pct()` / `cls()` 輔助函式，全數轉義；
  狀態與優先級改用白名單對照表。
- **舊版 JSON 匯入後白畫面**：v1.0 檔案缺 `outcomes` / `suggestions`，
  render 時拋 TypeError。新增 `normalizeData()` 自動補齊所有缺漏欄位。
- **刪除留下孤兒紀錄**：刪策略只 cascade 刪 action，KPI 與成效紀錄殘留。
  新增 `cascadeDelete()` 完整清理關聯資料。
- **重設資料殘留**：原 `resetData()` 未涵蓋 v2.0 新增欄位。
- **`|| 0` 短路 bug**：數值為 0 時被誤判為空值。
- **`renderSlide()` 無 undefined 防護**。

### Added

- **成效追蹤**頁面：記錄策略執行結果（完成率、評分 1-5、經驗教訓）
- **改進建議**頁面：管理改進建議生命週期（待處理／已接受／已拒絕／已實施）
- 儀表板新增成效統計卡片
- 簡報模式新增成效追蹤頁面
- 資料毀損時降級為空白 + 明示提示（不再靜默載入半殘資料）
- 匯入時提示是否已自動補齊舊版欄位
- 刪除確認訊息列出連帶刪除的項目數

### Changed

- `schema.json` 同步至 v2.0：新增 `outcomes` / `suggestions` 定義
- `meta.version` 由 `1.0` 改為 `2.0`

### 資料遷移說明

v1.0 的 JSON 檔案**不需要**手動轉換。`normalizeData()` 會在載入與匯入時
自動補齊缺少的欄位，並將版本標記升為 2.0。

---

## [1.1.0] - 2026-10-02

### Added

- 整合遞迴自我改進模組：成效追蹤 + 改進建議
- `recursive-self-improvement.html` 概念規格書

---

## [1.0.0] - 2026-10-02

### Added

- 儀表板：統計概覽、最近行動方案、即將到期 KPI
- 願景與使命：公司基本設定、核心價值觀管理
- SWOT 分析：四象限編輯（優勢/劣勢/機會/威脅）
- 數據現況：指標管理（財務/客戶/內部流程/學習成長）
- 策略主題：優先級與狀態追蹤
- 行動方案：負責人、時程、進度追蹤
- KPI 追蹤：現況 vs 目標、達成率計算
- 簡報模式：一鍵生成完整簡報，鍵盤導航
- 資料管理：localStorage 自動儲存、JSON 匯出/匯入
- 響應式設計：支援桌面、平板、手機
- Midnight Executive 深色主題

### Technical

- 單檔 HTML 應用（HTML + CSS + JS）
- 零外部依賴
- GitHub Pages 部署
- JSON Schema 資料模型定義

---

## [Unreleased]

### Planned

- 自動推導改進建議（從成效紀錄主動發現問題，門檻值可調）
- 多人即時協作（WebSocket）
- 雲端同步（Firebase）
- 歷史版本管理
- 圖表視覺化
- 簡報匯出 PDF
- 多語言支援（英文）

---

> Built with ❤️ by share543