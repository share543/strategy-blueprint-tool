# 策略藍圖發展工具 (Strategy Blueprint Tool)

> 公司策略規劃與執行的完整解決方案 — 從願景到 KPI 的一站式管理平台

[![GitHub](https://img.shields.io/badge/GitHub-share543%2Fstrategy--blueprint--tool-blue)](https://github.com/share543/strategy-blueprint-tool)
[![License](https://img.shields.io/badge/License-MIT-green)](https://github.com/share543/strategy-blueprint-tool/blob/master/LICENSE)
[![Pages](https://img.shields.io/badge/GitHub%20Pages-Live-brightgreen)](https://share543.github.io/strategy-blueprint-tool/)

---

**目前版本：v2.0.0** — 已整合遞迴自我改進（成效追蹤 + 改進建議）

## 📋 目錄

- [專案簡介](#專案簡介)
- [核心功能](#核心功能)
- [快速開始](#快速開始)
- [使用指南](#使用指南)
- [資料模型](#資料模型)
- [資料相容性](#資料相容性)
- [技術架構](#技術架構)
- [部署方式](#部署方式)
- [開發指南](#開發指南)
- [版本規劃](#版本規劃)
- [授權](#授權)

---

## 專案簡介

### 解決的問題

企業在年度策略規劃時常見痛點：

| 痛點 | 本工具的解決方案 |
|------|------------------|
| 各部門各自發想，缺乏統一框架 | 混合型策略框架（願景→SWOT→策略→行動→KPI） |
| 策略無法追蹤執行進度 | 行動方案 + KPI 追蹤 + 進度可視化 |
| 簡報製作耗時 | 一鍵簡報模式，自動生成完整簡報 |
| 資料散落各處 | 統一 JSON 資料模型，可匯出備份 |
| 缺乏數據支撐 | 數據現況模組，強制輸入基礎依據 |

### 適用場景

- ✅ 年度策略規劃會議
- ✅ 部門目標對齊
- ✅ 向董事長/董事會展示
- ✅ 策略執行追蹤
- ✅ 跨部門協作

### 設計理念

```
願景/使命
    ↓
環境分析（SWOT + 數據現況）
    ↓
策略主題（3-5 個）
    ↓
行動方案（每個主題 2-4 個）
    ↓
KPI + 目標值 + 負責人
```

---

## 核心功能

### 1. 儀表板 (Dashboard)

- 統計概覽：策略主題數、行動方案數、KPI 數、整體進度
- 最近行動方案：快速查看最新動態
- 即將到期 KPI：自動提醒緊迫事項

### 2. 願景與使命

- 公司名稱與年度設定
- 使命 (Mission) 與願景 (Vision)
- 核心價值觀管理

### 3. SWOT 分析

- 四象限編輯：優勢、劣勢、機會、威脅
- 動態新增/刪除/修改
- 即時預覽

### 4. 數據現況

- 指標管理：財務、客戶、內部流程、學習成長
- 數值 + 單位 + 備註
- 搜尋與篩選功能

### 5. 策略主題

- 策略標題、描述、優先級（高/中/低）
- 狀態追蹤：草案、進行中、已完成、暫停
- 關聯行動方案計數

### 6. 行動方案

- 方案標題、描述、負責人
- 時程管理：開始/結束日期
- 進度追蹤：0-100%
- 狀態管理：未開始、進行中、已完成、暫停

### 7. KPI 追蹤

- 現況值 vs 目標值
- 自動計算達成率
- 期限提醒
- 進度條可視化

### 8. 成效追蹤（v1.1+）

- 記錄每期策略執行結果：完成率、評分（1-5）、經驗教訓
- 統計卡片：成效紀錄數、平均評分、平均完成率
- 支援期間標記（例：2026-Q4），可跨期比較
- **這是遞迴改進的輸入** —— 有資料才能找出問題

### 9. 改進建議（v1.1+）

- 管理改進建議的生命週期：待處理 → 已接受 → 已拒絕 → 已實施
- 優先級分級（高/中/低）
- 統計卡片：待處理、已實施、已拒絕數量
- **這是遞迴改進的產出** —— 把成效問題轉成具體行動

### 10. 簡報模式

- 一鍵生成完整簡報（最多 9 頁）
- 自動排版：封面 → 願景 → SWOT → 數據 → 策略 → 行動 → KPI → 成效 → 結尾
- 鍵盤導航：方向鍵/空白鍵切換，ESC 退出
- 響應式設計，適合各種螢幕

### 11. 資料管理

- 自動儲存：瀏覽器 localStorage
- 匯出：JSON 格式，可備份、可版本管理
- 匯入：從 JSON 檔案還原
- 重設：清空所有資料

---

## 快速開始

### 線上使用（推薦）

直接開啟：**https://share543.github.io/strategy-blueprint-tool/**

無需安裝、無需帳號、免伺服器。

### 本地使用

1. 下載 `index.html`
2. 用瀏覽器開啟（Chrome、Edge、Firefox、Safari）
3. 開始使用

### 系統需求

| 需求 | 規格 |
|------|------|
| 瀏覽器 | Chrome 90+、Edge 90+、Firefox 88+、Safari 14+ |
| 螢幕解析度 | 1024×768 以上 |
| 網路 | 僅首次載入需要（GitHub Pages） |
| 儲存 | 瀏覽器 localStorage（約 5MB） |

---

## 使用指南

### 基本流程

```
步驟 1：設定公司資訊
    ↓
步驟 2：填寫願景與使命
    ↓
步驟 3：完成 SWOT 分析
    ↓
步驟 4：輸入數據現況
    ↓
步驟 5：制定策略主題
    ↓
步驟 6：規劃行動方案
    ↓
步驟 7：設定 KPI 追蹤
    ↓
步驟 8：生成簡報
```

### 操作說明

#### 新增項目

1. 點擊頁面右上角「+ 新增」按鈕
2. 填寫表單
3.點擊「儲存」

#### 編輯項目

1. 點擊項目右側的 ✏️ 圖示
2. 修改內容
3. 點擊「儲存」

#### 刪除項目

1. 點擊項目右側的 🗑️ 圖示
2. 確認刪除

#### 搜尋與篩選

- 使用搜尋框快速找到項目
- 使用篩選按鈕按狀態/分類篩選

#### 簡報模式

1. 點擊左側選單「簡報模式」
2. 點擊「開始簡報」
3. 使用方向鍵或按鈕切換頁面
4. 按 ESC 退出

### 快捷鍵

| 按鍵 | 功能 |
|------|------|
| → / 空白鍵 | 下一頁簡報 |
| ← | 上一頁簡報 |
| ESC | 退出簡報模式 |

---

## 資料模型

### 完整結構

```json
{
  "meta": {
    "companyName": "公司名稱",
    "year": 2027,
    "lastUpdated": "2026-10-02T14:00:00.000Z",
    "version": "1.0"
  },
  "vision": {
    "mission": "使命",
    "vision": "願景",
    "values": ["價值觀1", "價值觀2"]
  },
  "swot": {
    "strengths": ["優勢1", "優勢2"],
    "weaknesses": ["劣勢1", "劣勢2"],
    "opportunities": ["機會1", "機會2"],
    "threats": ["威脅1", "威脅2"]
  },
  "metrics": [
    {
      "id": "m1234567890",
      "name": "營收",
      "value": 50000,
      "unit": "萬元",
      "category": "財務",
      "note": "2025 年實績"
    }
  ],
  "strategies": [
    {
      "id": "s1234567890",
      "title": "策略標題",
      "description": "策略描述",
      "priority": "高",
      "status": "進行中"
    }
  ],
  "actions": [
    {
      "id": "a1234567890",
      "strategyId": "s1234567890",
      "title": "行動方案標題",
      "description": "行動方案描述",
      "owner": "負責人",
      "startDate": "2027-01-01",
      "endDate": "2027-06-30",
      "status": "進行中",
      "progress": 50
    }
  ],
  "kpis": [
    {
      "id": "k1234567890",
      "actionId": "a1234567890",
      "name": "KPI 名稱",
      "currentValue": 25000,
      "targetValue": 50000,
      "unit": "萬元",
      "deadline": "2027-06-30"
    }
  ],
  "outcomes": [
    {
      "id": "o1234567890",
      "strategyId": "s1234567890",
      "period": "2026-Q4",
      "completionRate": 62,
      "score": 4,
      "notes": "原廠回應緩慢，需加強溝通"
    }
  ],
  "suggestions": [
    {
      "id": "sg1234567890",
      "issue": "系統導入進度落後",
      "suggestion": "增加專人負責需求蒐集與驗收",
      "priority": "高",
      "status": "待處理"
    }
  ]
}
```

### 資料關聯圖

```
meta (公司資訊)
    ↓
vision (願景/使命)
    ↓
swot (環境分析) ← metrics (數據現況)
    ↓
strategies (策略主題)
    ↓
actions (行動方案)
    ↓
kpis (KPI 追蹤)

strategies ← outcomes (成效追蹤) → suggestions (改進建議)
   ↑              ↑                    │
   └──────────────┴────────────────────┘
        下一輪策略修正
```

### 識別碼規則

| 類型 | 前綴 | 範例 |
|------|------|------|
| 指標 | `m` | `m1696252800000` |
| 策略 | `s` | `s1696252800000` |
| 行動 | `a` | `a1696252800000` |
| KPI | `k` | `k1696252800000` |
| 成效 | `o` | `o1696252800000` |
| 建議 | `sg` | `sg1696252800000` |

### 刪除的 cascade 規則

刪除上層項目會連帶清理下層，避免孤兒紀錄讓數字失真：

| 刪除 | 連帶刪除 | 不刪除 |
|------|---------|--------|
| 策略 | 該策略下所有行動 → 指向那些行動的 KPI → 該策略的成效 | 改進建議（跨策略，由你自行判斷） |
| 行動 | 指向它的 KPI | 成效紀錄（掛在策略上） |

---

## 資料相容性

### 舊版資料不需要手動轉換

v1.0（2026-10-02）的 JSON 檔案可以直接在 v2.0 打開。`normalizeData()`
會在載入與匯入時自動補齊缺少的欄位，並把版本標記升為 2.0。

若匯入的是舊檔，工具會提示「已自動補齊舊版缺少的欄位」。

### 各版本的欄位差異

| 欄位 | v1.0 | v2.0 | 遷移行為 |
|------|------|------|---------|
| meta / vision / swot | ✓ | ✓ | 不變 |
| metrics / strategies / actions / kpis | ✓ | ✓ | 不變 |
| outcomes | ✗ | ✓ | 自動補 `[]` |
| suggestions | ✗ | ✓ | 自動補 `[]` |
| meta.version | `1.0` | `2.0` | 自動升級 |

### 資料毡損時的行為

`localStorage` 內容若無法解析，工具會：
1. 在 console 記錄錯誤
2. 降級為空白資料（不清除原始儲存，之後仍可匯入復原）
3. 顯示提示訊息告知使用者

---

## 技術架構

### 技術棧

| 層級 | 技術 | 說明 |
|------|------|------|
| 前端 | 原生 HTML/CSS/JavaScript | 無框架依賴，輕量快速 |
| 儲存 | Browser localStorage | 客戶端持久化 |
| 部署 | GitHub Pages | 靜態託管，全球 CDN |
| 版本控制 | Git + GitHub | 協作與版本管理 |

### 架構圖

```
┌─────────────────────────────────────────┐
│              瀏覽器 (Client)              │
├─────────────────────────────────────────┤
│  ┌─────────┐  ┌─────────┐  ┌─────────┐ │
│  │ 儀表板  │  │ 編輯器  │  │ 簡報模式│ │
│  └────┬────┘  └────┬────┘  └────┬────┘ │
│       └─────────────┼─────────────┘     │
│                     ↓                   │
│            ┌─────────────────┐          │
│            │  資料管理層     │          │
│            │  (localStorage) │          │
│            └────────┬────────┘          │
│                     ↓                   │
│            ┌─────────────────┐          │
│            │  JSON 匯出/匯入 │          │
│            └─────────────────┘          │
└─────────────────────────────────────────┘
```

### 檔案結構

```
strategy-blueprint-tool/
├── index.html                    # 主程式（單檔應用，約 98KB）
├── schema.json                   # 資料模型定義 v2.0
├── README.md                     # 本文件
├── TECH_SPEC.md                  # 技術規格書
├── CHANGELOG.md                  # 版本變更紀錄
├── HANDOFF.md                    # 交接文件
├── LICENSE                       # MIT 授權
└── recursive-self-improvement.html  # 遞迴改進概念規格書（功能已內建，頁面保留供參考）
```

### 設計模式

- **單頁應用 (SPA)**：所有功能在單一 HTML 檔案
- **資料驅動**：UI 自動從資料模型渲染
- **響應式設計**：支援桌面、平板、手機
- **離線優先**：資料儲存於本地，可離線使用

### 安全性

- 資料僅儲存於使用者瀏覽器本地
- 無伺服器端資料傳輸
- 無第三方追蹤
- 支援 Content Security Policy

---

## 部署方式

### GitHub Pages（官方）

本工具已部署於 GitHub Pages：

**https://share543.github.io/strategy-blueprint-tool/**

### 自架部署

#### 方法 1：GitHub Pages

1. Fork 本專案
2. 進入 Settings → Pages
3. Source 選擇 `master` 分支
4. 等待部署完成（約 1-2 分鐘）

#### 方法 2：任何靜態伺服器

```bash
# 使用 Python 簡易伺服器
cd strategy-blueprint-tool
python3 -m http.server 8000

# 使用 Node.js http-server
npx http-server -p 8000

# 使用 Nginx
# 將檔案放入 /var/www/html/strategy-blueprint-tool/
```

#### 方法 3：Docker

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/
COPY schema.json /usr/share/nginx/html/
EXPOSE 80
```

```bash
docker build -t strategy-blueprint-tool .
docker run -p 8080:80 strategy-blueprint-tool
```

---

## 開發指南

### 環境設定

```bash
# Clone 專案
git clone https://github.com/share543/strategy-blueprint-tool.git
cd strategy-blueprint-tool

# 啟動本地伺服器
python3 -m http.server 8000
# 或
npx http-server
```

### 開發流程

1. **修改 `index.html`**：所有程式碼在此檔案
2. **整理資料模型**：更新 `schema.json`
3. **測試**：用瀏覽器開啟 `http://localhost:8000`
4. **提交**：`git add . && git commit -m "描述"`
5. **推送**：`git push origin master`

### 程式碼結構

```javascript
// 資料模型
let data = { ... };

// 初始化
document.addEventListener('DOMContentLoaded', function() {
    loadData();
    initNavigation();
    renderDashboard();
});

// 核心功能模組
- loadData() / saveData()      // 資料持久化
- initNavigation()             // 導航初始化
- switchPage()                 // 頁面切換
- renderDashboard()            // 儀表板渲染
- renderVision()               // 願景渲染
- renderSwot()                 // SWOT 渲染
- renderMetrics()              // 指標渲染
- renderStrategies()           // 策略渲染
- renderActions()              // 行動方案渲染
- renderKpis()                 // KPI 渲染
- startPresentation()          // 簡報模式
- exportData() / importData()  // 匯出匯入
```

### 新增功能檢查清單

- [ ] 更新 `schema.json` 資料模型
- [ ] 在 `index.html` 新增 HTML 結構
- [ ] 新增 CSS 樣式
- [ ] 新增 JavaScript 渲染函數
- [ ] 新增 CRUD 操作
- [ ] 更新導航選單
- [ ] 更新簡報模式
- [ ] 測試所有功能
- [ ] 更新文件

---

## 版本規劃

### v2.0（目前版本 — 2026-10-04）

- ✅ 儀表板
- ✅ 願景與使命
- ✅ SWOT 分析
- ✅ 數據現況
- ✅ 策略主題
- ✅ 行動方案
- ✅ KPI 追蹤
- ✅ **成效追蹤**（遞迴改進的輸入）
- ✅ **改進建議**（遞迴改進的產出）
- ✅ 簡報模式（9 頁）
- ✅ JSON 匯出/匯入 + 舊版資料自動遷移
- ✅ XSS 防護（全部使用者輸入轉義）

### v2.1（規劃中）

- [ ] **自動推導改進建議** —— 從成效紀錄主動發現問題（完成率過低、評分偏低的策略自動產生建議草稿，門檻值可調）
- [ ] 歷史趨勢圖表（跨期比較完成率與評分變化）
- [ ] 資料健康檢查（提醒未指派負責人、KPI 無時程等）
- [ ] 深色/淺色主題切換
- [ ] 簡報匯出 PDF
- [ ] 多語言支援（英文）

### v3.0（規劃中）

- [ ] 多人即時協作（WebSocket）
- [ ] 雲端同步（Firebase）
- [ ] 歷史版本管理
- [ ] 圖表視覺化（Chart.js）
- [ ] 權限管理

---

## 授權

MIT License — 可自由使用、修改、散布。

Copyright (c) 2026 Arthur Hu (share543)

---

## 聯絡

- **專案首頁**：https://github.com/share543/strategy-blueprint-tool
- **線上展示**：https://share543.github.io/strategy-blueprint-tool/
- **問題回報**：https://github.com/share543/strategy-blueprint-tool/issues

---

> Built with ❤️ by share543
