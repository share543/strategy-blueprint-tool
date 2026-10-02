# Handoff — 策略藍圖發展工具

> 2026-10-02 交接文件。換電腦後接手用。

---

## 專案狀態：✅ 已完成部署

**Repo：** https://github.com/share543/strategy-blueprint-tool
**Page：** https://share543.github.io/strategy-blueprint-tool/
**站內：** https://share543.com/ai/strategy-blueprint-tool/

---

## 這次做了什麼

1. **建立工具** — 從零開發「策略藍圖發展工具」v1.0
   - 混合型策略框架：願景 → SWOT → 數據 → 策略 → 行動 → KPI
   - 8 個功能模組 + 簡報模式
   - 單檔 HTML（73KB），零外部依賴
   - Midnight Executive 深色主題

2. **完善文件**
   - `README.md` — 使用說明（12.6KB）
   - `TECH_SPEC.md` — 技術規格書（12.9KB）
   - `CHANGELOG.md` — 版本變更紀錄
   - `LICENSE` — MIT 授權

3. **部署到 share543 網站**
   - 在 `sync-github-repos.py` 新增策展內容
   - 執行完整更新管線（sync → scan → build → validate → check-links）
   - 本機驗證：HTTP 200 ✓、縮圖 ✓、meta.json ✓
   - 全站 153/0 連結全綠

---

## 關鍵檔案位置

| 檔案 | 路徑 |
|------|------|
| 工具本體 | `~/obsidian-vault/Archive/knowledge/work/strategy-blueprint-tool/index.html` |
| 資料模型 | `~/obsidian-vault/Archive/knowledge/work/strategy-blueprint-tool/schema.json` |
| 站內頁面 | `~/web-server/projects/ai/strategy-blueprint-tool/` |
| 策展內容 | `~/web-server/scripts/sync-github-repos.py`（`REPO_CONTENT` 字典） |

---

## 接手第一步

```bash
# 1. Clone repo（如果新電腦還沒有）
git clone https://github.com/share543/strategy-blueprint-tool.git

# 2. 確認 share543 網站狀態
cd ~/web-server
node scripts/scan-projects.mjs
/usr/bin/python3 scripts/build-list-pages.py
node scripts/check-links.mjs

# 3. 本機測試
python3 -m http.server 8000
# 開啟 http://localhost:8000/ai/strategy-blueprint-tool/
```

---

## 下一步規劃（v1.1）

- [ ] 多語言支援（英文）
- [ ] 簡報匯出 PDF
- [ ] 資料驗證與提示
- [ ] 深色/淺色主題切換
- [ ] 多人即時協作（WebSocket）
- [ ] 雲端同步（Firebase）
- [ ] 歷史版本管理
- [ ] 圖表視覺化（Chart.js）

---

## 環境陷阱提醒

| 陷阱 | 正確寫法 |
|------|----------|
| `python3` 是 Hermes 3.14，沒有 PIL | 用 `/usr/bin/python3` |
| `PYTHONPATH` 洩漏 | 用 `env -u PYTHONPATH /usr/bin/python3` |
| `systemctl reload caddy` 會失敗 | 用 `caddy reload --config config/Caddyfile` |
| 本機 DNS 無法解析 `share543.com` | 用 `localhost:3000` 測試 |

---

## 建議載入的 Skills

- `share543-website-management` — 動 share543 網站時
- `caddy-web-server` — 動 Caddy 設定時
- `github` — 推 PR / 開 issue 時
- `hermes-agent` — 設定 Hermes 時

---

> Built with ❤️ by share543
