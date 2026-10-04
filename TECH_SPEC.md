# 技術規格書 — 策略藍圖發展工具

> Strategy Blueprint Tool Technical Specification v2.0

---

## 1. 系統概述

| 項目 | 規格 |
|------|------|
| 系統名稱 | 策略藍圖發展工具 (Strategy Blueprint Tool) |
| 版本 | 2.0.0 |
| 架構 | 單頁應用 (SPA) |
| 部署 | GitHub Pages (靜態託管) |
| 相依性 | 無（零外部套件） |
| 瀏覽器支援 | Chrome 90+, Edge 90+, Firefox 88+, Safari 14+ |

---

## 2. 檔案結構

```
strategy-blueprint-tool/
├── index.html                    # 主程式（HTML + CSS + JS 單檔，約 98KB）
├── schema.json                   # 資料模型定義 v2.0 (JSON Schema)
├── README.md                     # 使用說明
├── TECH_SPEC.md                  # 本文件
├── CHANGELOG.md                  # 版本變更紀錄
├── HANDOFF.md                    # 交接文件
├── LICENSE                       # MIT 授權
└── recursive-self-improvement.html  # 概念規格書（功能已內建）
```

---

## 3. 資料模型

### 3.1 頂層結構

```typescript
interface StrategyBlueprint {
  meta: Meta;
  vision: Vision;
  swot: Swot;
  metrics: Metric[];
  strategies: Strategy[];
  actions: Action[];
  kpis: Kpi[];
  outcomes: Outcome[];        // v2.0 新增 —— 遞迴改進的輸入
  suggestions: Suggestion[];  // v2.0 新增 —— 遞迴改進的產出
}

/**
 * 資料正規化 —— v1.0 → v2.0 的遷移點。
 * 舊版 JSON 缺 outcomes / suggestions，直接 render 會拋
 * TypeError: Cannot read properties of undefined (reading 'length')
 */
function normalizeData(raw: object): StrategyBlueprint;  // 補齊所有欄位 + 升版
function blankData(): StrategyBlueprint;                 // 空資料的單一來源
```

### 3.2 各模組定義

#### Meta

| 欄位 | 類型 | 必填 | 說明 |
|------|------|------|------|
| companyName | string | ✓ | 公司名稱 |
| year | number | ✓ | 年度 |
| lastUpdated | string (ISO 8601) | ✓ | 最後更新時間 |
| version | string | ✓ | 資料格式版本 |

#### Vision

| 欄位 | 類型 | 必填 | 說明 |
|------|------|------|------|
| mission | string | ✓ | 使命 |
| vision | string | ✓ | 願景 |
| values | string[] | ✓ | 核心價值觀 |

#### Swot

| 欄位 | 類型 | 必填 | 說明 |
|------|------|------|------|
| strengths | string[] | ✓ | 優勢 |
| weaknesses | string[] | ✓ | 劣勢 |
| opportunities | string[] | ✓ | 機會 |
| threats | string[] | ✓ | 威脅 |

#### Metric

| 欄位 | 類型 | 必填 | 說明 |
|------|------|------|------|
| id | string | ✓ | 唯一識別碼 (前綴 `m`) |
| name | string | ✓ | 指標名稱 |
| value | number | ✓ | 數值 |
| unit | string | ✓ | 單位 |
| category | string | ✓ | 分類：財務/客戶/內部流程/學習成長 |
| note | string | | 備註 |

#### Strategy

| 欄位 | 類型 | 必填 | 說明 |
|------|------|------|------|
| id | string | ✓ | 唯一識別碼 (前綴 `s`) |
| title | string | ✓ | 策略標題 |
| description | string | ✓ | 策略描述 |
| priority | enum | ✓ | 優先級：高/中/低 |
| status | enum | ✓ | 狀態：草案/進行中/已完成/暫停 |

#### Action

| 欄位 | 類型 | 必填 | 說明 |
|------|------|------|------|
| id | string | ✓ | 唯一識別碼 (前綴 `a`) |
| strategyId | string | ✓ | 所屬策略 ID |
| title | string | ✓ | 方案標題 |
| description | string | ✓ | 方案描述 |
| owner | string | ✓ | 負責人 |
| startDate | string (date) | | 開始日期 |
| endDate | string (date) | | 結束日期 |
| status | enum | ✓ | 狀態：未開始/進行中/已完成/暫停 |
| progress | number | ✓ | 進度 0-100 |

#### Kpi

| 欄位 | 類型 | 必填 | 說明 |
|------|------|------|------|
| id | string | ✓ | 唯一識別碼 (前綴 `k`) |
| actionId | string | ✓ | 所屬行動方案 ID |
| name | string | ✓ | KPI 名稱 |
| currentValue | number | ✓ | 現況值 |
| targetValue | number | ✓ | 目標值 |
| unit | string | ✓ | 單位 |
| deadline | string (date) | | 期限 |

#### Outcome（v2.0 新增）

成效追蹤紀錄 —— 遞迴自我改進的**輸入**。

| 欄位 | 類型 | 必填 | 說明 |
|------|------|------|------|
| id | string | ✓ | 唯一識別碼 (前綴 `o`) |
| strategyId | string | ✓ | 所屬策略 ID |
| period | string | | 期間標記，例：2026-Q4 |
| completionRate | number | ✓ | 完成率 0-100 |
| score | number | ✓ | 成效評分 1-5 |
| notes | string | | 備註 / 經驗教訓 |

#### Suggestion（v2.0 新增）

改進建議 —— 遞迴自我改進的**產出**。

| 欄位 | 類型 | 必填 | 說明 |
|------|------|------|------|
| id | string | ✓ | 唯一識別碼 (前綴 `sg`) |
| issue | string | ✓ | 問題描述 |
| suggestion | string | ✓ | 改進建議內容 |
| priority | enum | ✓ | 優先級：高/中/低 |
| status | enum | ✓ | 待處理/已接受/已拒絕/已實施 |

---

## 3.3 關聯圖與 cascade 規則

```
strategies ──┬── actions ──── kpis
             │
             └── outcomes ──── suggestions（跨策略，不隨刪除自動移除）
```

| 刪除目標 | 連帶刪除 | 保留 |
|---------|---------|------|
| 策略 | 該策略下所有 actions → 指向那些 action 的 kpis → 該策略的 outcomes | suggestions |
| action | 指向它的 kpis | outcomes（掛在 strategy 上） |

**理由**：孤兒紀錄會讓儀表板與簡報的數字失真 —— 這是要拿給管理層看的東西。

---

## 4. 儲存層

### 4.1 儲存機制

| 項目 | 規格 |
|------|------|
| 技術 | Browser localStorage |
| Key | `strategyBlueprint` |
| 格式 | JSON |
| 容量限制 | 約 5MB |
| 生命週期 | 永久（除非手動清除） |

### 4.2 儲存策略

```javascript
// 讀取
const saved = localStorage.getItem('strategyBlueprint');
data = JSON.parse(saved);

// 寫入
data.meta.lastUpdated = new Date().toISOString();
localStorage.setItem('strategyBlueprint', JSON.stringify(data));
```

### 4.3 匯出/匯入

| 操作 | 格式 | 說明 |
|------|------|------|
| 匯出 | JSON 檔 | `strategy-blueprint-{year}.json` |
| 匯入 | JSON 檔案 | 檔案選擇器讀取 |
| 重設 | — | 清空所有資料 |

---

## 5. UI 架構

### 5.1 頁面結構

```
┌─────────────────────────────────────────────┐
│                  側邊欄                      │
│  ┌─────────────────────────────────────┐    │
│  │ 📊 儀表板                            │    │
│  ├─────────────────────────────────────┤    │
│  │ 基礎設定                             │    │
│  │   🎯 願景與使命                      │    │
│  │   🔍 SWOT 分析                      │    │
│  │   📊 數據現況                        │    │
│  ├─────────────────────────────────────┤    │
│  │ 策略規劃                             │    │
│  │   🎯 策略主題                        │    │
│  │   ⚡ 行動方案                        │    │
│  │   📌 KPI 追蹤                       │    │
│  ├─────────────────────────────────────┤    │
│  │ 輸出                                │    │
│  │   🎬 簡報模式                        │    │
│  └─────────────────────────────────────┘    │
└─────────────────────────────────────────────┘
        ↓ 切換
┌─────────────────────────────────────────────┐
│                 主內容區                     │
│  ┌─────────────────────────────────────┐    │
│  │ 工具列 (標題 + 操作按鈕)             │    │
│  ├─────────────────────────────────────┤    │
│  │                                     │    │
│  │           頁面內容                   │    │
│  │                                     │    │
│  └─────────────────────────────────────┘    │
└─────────────────────────────────────────────┘
```

### 5.2 設計系統

#### 色彩系統

```css
:root {
  --primary: #E8447A;      /* 主色調 - 洋紅 */
  --secondary: #F5B301;    /* 次要色 - 金黃 */
  --dark: #2B2B33;         /* 深色背景 */
  --light: #E8F3FB;        /* 淺色文字 */
  --bg: #1a1a2e;           /* 主背景 */
  --card-bg: #252540;      /* 卡片背景 */
  --text: #E8F3FB;         /* 文字顏色 */
  --text-muted: #8892b0;   /* 次要文字 */
  --success: #00C9A7;      /* 成功/優勢 */
  --warning: #F5B301;      /* 警告/機會 */
  --danger: #E8447A;       /* 危險/劣勢 */
}
```

#### 字體系統

```css
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Microsoft JhengHei', sans-serif;
```

| 元素 | 字體大小 | 粗細 |
|------|----------|------|
| 標題 h1 | 24px | Bold |
| 標題 h2 | 18px | SemiBold |
| 內文 | 14px | Regular |
| 次要文字 | 12px | Regular |
| 標籤 | 11px | Medium |

#### 間距系統

| 等級 | 數值 | 用途 |
|------|------|------|
| xs | 4px | 圖示間距 |
| sm | 8px | 元素內距 |
| md | 16px | 卡片內距 |
| lg | 24px | 區塊間距 |
| xl | 32px | 頁面內距 |

---

## 6. 核心模組

### 6.1 資料管理層

```javascript
// 全域資料物件
let data = { /* StrategyBlueprint */ };

// 正規化 —— v1.0 → v2.0 遷移的關鍵
function normalizeData(raw) {
  // 逐欄位檢查型別，缺漏就補預設值（陣列補 []、字串補 ''、物件補 {}）
  // 同時把 meta.version 升為 '2.0'
  return d;
}
function blankData() { /* 空資料的單一來源 */ }

// 生命週期
function loadData()    { /* localStorage → normalizeData() → data */ }
function saveData()    { /* data → localStorage */ }
function countItems(d) { /* 統計各類項目數，用於匯入訊息 */ }

// 刪除時的關聯清理
function cascadeDelete({ strategyId, actionId }) {
  // 刪策略 → strategies + actions + kpis + outcomes
  // 刪行動 → actions + kpis
  // suggestions 不動（跨策略，由使用者判斷）
}
```

### 6.2 導航層

```javascript
// 頁面切換
function switchPage(page) {
  // 更新側邊欄 active 狀態
  // 隱藏所有頁面
  // 顯示目標頁面
  // 呼叫對應渲染函數
}
```

### 6.3 渲染層

| 函數 | 說明 |
|------|------|
| `renderDashboard()` | 儀表板統計與最近動態 |
| `renderVision()` | 願景與使命表單 |
| `renderSwot()` | SWOT 四象限列表 |
| `renderMetrics()` | 指標列表 + 篩選 |
| `renderStrategies()` | 策略列表 + 篩選 |
| `renderActions()` | 行動方案列表 + 篩選 |
| `renderKpis()` | KPI 列表 |
| `renderOutcomes()` | 成效追蹤列表 + 統計（v2.0） |
| `renderSuggestions()` | 改進建議列表 + 統計（v2.0） |
| `renderValues()` | 價值觀列表 |
| `renderSlide()` | 簡報頁面渲染 |

### 6.4 編輯層

| 函數 | 說明 |
|------|------|
| `openMetricModal()` | 開啟指標編輯 Modal |
| `openStrategyModal()` | 開啟策略編輯 Modal |
| `openActionModal()` | 開啟行動方案編輯 Modal |
| `openKpiModal()` | 開啟 KPI 編輯 Modal |
| `openOutcomeModal()` | 開啟成效編輯 Modal（v2.0） |
| `openSuggestionModal()` | 開啟建議編輯 Modal（v2.0） |

### 6.5 簡報層

```javascript
function startPresentation() {
  slides = generateSlides();  // 從資料生成簡報頁面
  currentSlide = 0;
  // 進入簡報模式
}

function generateSlides() {
  // 封面 → 願景 → SWOT → 數據 → 策略 → 行動 → KPI → 結尾
}
```

---

## 7. 事件處理

### 7.1 DOM 事件

| 事件 | 元素 | 處理 |
|------|------|------|
| click | nav-item | switchPage() |
| click | btn (新增) | openXxxModal() |
| click | btn-edit | editXxx() |
| click | btn-delete | deleteXxx() |
| change | form-control | saveData() |
| input | search | renderXxx() |
| click | filter-btn | filterXxx() |

### 7.2 鍵盤事件

| 按鍵 | 模式 | 功能 |
|------|------|------|
| → / Space | 簡報 | nextSlide() |
| ← | 簡報 | prevSlide() |
| ESC | 簡報 | exitPresentation() |

---

## 8. 安全性

| 項目 | 措施 |
|------|------|
| 資料儲存 | 僅存本地 localStorage，無網路傳輸 |
| **XSS 防護** | 所有使用者輸入經 `esc()` 轉義後才進 `innerHTML`，**包含屬性值**（`value="..."`）與 `<option>` 標籤 |
| **CSS class 注入** | 狀態/優先級經 `STATUS_CLASS` / `PRIORITY_CLASS` 白名單對照，不讓使用者字串直接成為 class |
| **數值處理** | `num()` 過濾 NaN、`pct()` 夾限範圍，避免 `undefined` / `Infinity` 進畫面 |
| **資料完整性** | `normalizeData()` 保證結構完整；`cascadeDelete()` 清理關聯紀錄 |
| 毀損資料 | 降級為空白 + 明示提示，不靜默載入半殘資料 |
| CSP | 支援 Content Security Policy |
| 依賴 | 零外部套件，無供應鏈風險 |

### XSS 測試方法（重要）

`innerHTML` 裡的 `<script>` 標籤**不會**執行，但 `<img src=x onerror=...>` **會**。
測試時務必用 img/onerror 驗證 —— 用 script 會得到假的「安全」結論。

```javascript
// 驗證方式
data.strategies.push({ id:'x', title:'<img src=x onerror="window.__XSS=1">', ... });
renderStrategies();
// 檢查：document.querySelector('img[onerror]') 應為 null，且 window.__XSS 應為 0
```

### 輔助函式

| 函式 | 用途 |
|------|------|
| `esc(s)` | HTML 轉義（`& < > " '` → 實體） |
| `num(v, d)` | 解析為數值，NaN 回退預設值 |
| `pct(v, max)` | 夾限在 0..max 的數值 |
| `cls(v, map, fallback)` | 白名單 class 對照 |

---

## 9. 效能

| 項目 | 目標 |
|------|------|
| 首次載入 | < 1 秒（GitHub Pages CDN） |
| 本地儲存 | < 100ms（1000 筆資料） |
| 渲染 | < 16ms（60fps） |
| 檔案大小 | < 100KB |

### 優化策略

- 單檔打包，減少 HTTP 請求
- CSS 使用 CSS Variables，減少重複
- JS 使用事件委派
- 搜尋/篩選採用即時渲染

---

## 10. 瀏覽器相容性

| 瀏覽器 | 最低版本 | 備註 |
|--------|----------|------|
| Chrome | 90+ | 完整支援 |
| Edge | 90+ | 完整支援 |
| Firefox | 88+ | 完整支援 |
| Safari | 14+ | 完整支援 |
| IE | — | 不支援 |

---

## 11. 部署

### GitHub Pages

```bash
# 設定 GitHub Pages
gh api repos/{owner}/{repo}/pages -X POST -f "source[branch]=master" -f "source[path]=/"
```

### 靜態伺服器

```bash
# Python
python3 -m http.server 8000

# Node.js
npx http-server -p 8000

# Nginx
# 將檔案放入 /var/www/html/
```

### Docker

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/
COPY schema.json /usr/share/nginx/html/
EXPOSE 80
```

---

## 12. 開發規範

### 12.1 程式碼風格

- 縮排：4 空格
- 命名：camelCase（函式/變數）、kebab-case（CSS class）
- 註解：JSDoc 風格

### 12.2 Git 規範

```
feat: 新增功能
fix: 修正錯誤
docs: 文件更新
style: 格式調整
refactor: 重構
test: 測試
chore: 其他
```

### 12.3 提交前檢查

- [ ] 功能正常運作
- [ ] 瀏覽器主控台無錯誤
- [ ] 文件已更新
- [ ] 程式碼已格式化

---

## 13. 測試清單

### 13.1 功能測試

| 模組 | 測試項目 |
|------|----------|
| 儀表板 | 統計數字正確、最近更新顯示 |
| 願景 | 公司資訊儲存、價值觀 CRUD |
| SWOT | 四象限 CRUD |
| 數據 | 指標 CRUD、篩選、搜尋 |
| 策略 | 策略 CRUD、篩選、搜尋 |
| 行動 | 方案 CRUD、篩選、搜尋、進度 |
| KPI | KPI CRUD、搜尋、進度計算 |
| 成效 | 成效 CRUD、統計計算（平均評分/完成率） |
| 建議 | 建議 CRUD、狀態篩選、統計計算 |
| 簡報 | 頁面生成、導航、退出、含成效頁 |
| 匯出/匯入 | JSON 格式正確、資料完整 |

### 13.2 資料完整性測試（v2.0 新增）

| 測試項 | 預期結果 |
|--------|---------|
| 匯入 v1.0 舊 JSON | 自動補齊欄位，十頁 render 無錯誤 |
| 匯入毀損 JSON | 降級為空白 + 顯示提示 |
| 刪除策略 | 連帶清除 actions / kpis / outcomes，suggestions 保留 |
| 刪除行動方案 | 連帶清除指向它的 kpis，outcomes 不受影響 |
| 重設資料 | 所有欄位歸零（含 v2.0 新增欄位） |
| 數值為 0 | 正確顯示 0，不被 `||` 誤判為空 |

### 13.3 安全測試

| 測試項 | 方法 | 預期結果 |
|--------|------|---------|
| XSS（文字） | 標題輸入 `<img src=x onerror="window.__XSS=1">` | 無 img 元素、`window.__XSS === 0`、原字串顯示為文字 |
| XSS（屬性） | 檢查 `value="..."` 是否有未轉義插值 | 全部經 `esc()` |
| XSS（option） | 檢查 `<option>` 標籤內容 | 全部經 `esc()` |
| class 注入 | 狀態設為 `"><script>` | 只顯示為文字，不產生新 class |
| NaN 顯示 | 目標值設為非數字 | 顯示 0 或預設值，不顯示 NaN |

> ⚠ **測 XSS 務必用 img/onerror，不要用 `<script>`** ——
> innerHTML 裡的 script 標籤本來就不會執行，會得到假的「安全」結論。

### 13.4 相容性測試

| 瀏覽器 | 測試項目 |
|--------|----------|
| Chrome | 所有功能 |
| Edge | 所有功能 |
| Firefox | 所有功能 |
| Safari | 所有功能 |

### 13.5 響應式測試

| 螢幕尺寸 | 測試項目 |
|----------|----------|
| 桌面 (>1024px) | 完整功能 |
| 平板 (768-1024px) | 自適應佈局 |
| 手機 (<768px) | 自適應佈局 |

---

## 14. 版本規劃

### v2.0（目前 — 2026-10-04）

- ✅ 完整功能模組（願景 → SWOT → 數據 → 策略 → 行動 → KPI）
- ✅ 成效追蹤 + 改進建議（遞迴自我改進）
- ✅ 簡報模式（9 頁）
- ✅ JSON 匯出/匯入 + 舊版資料自動遷移（`normalizeData`）
- ✅ XSS 防護（`esc()` + class 白名單 + `num()`/`pct()`）
- ✅ cascade 刪除（`cascadeDelete()`）

### v2.1（規劃中）

- [ ] **自動推導改進建議** —— 從成效紀錄主動發現問題，門檻值可調
- [ ] 歷史趨勢圖表（跨期比較）
- [ ] 資料健康檢查
- [ ] 深色/淺色主題切換
- [ ] 簡報匯出 PDF
- [ ] 多語言支援

### v3.0（規劃中）

- [ ] 多人協作（WebSocket）
- [ ] 雲端同步（Firebase）
- [ ] 歷史版本
- [ ] 圖表視覺化

---

> Technical Specification v2.0 — 2026-10-04
