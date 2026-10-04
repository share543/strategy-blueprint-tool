# Handoff — 策略藍圖發展工具

> 2026-10-04 交接文件（v2.0）。換電腦後接手用。

---

## 專案狀態：✅ 已完成 v2.0 並上線

**Repo：** https://github.com/share543/strategy-blueprint-tool
**Page：** https://share543.github.io/strategy-blueprint-tool/
**站內：** https://share543.com/ai/strategy-blueprint-tool/

---

## 工具是什麼

給管理層用的年度策略規劃工具，完整閉環：

```
願景 → SWOT → 數據現況 → 策略主題 → 行動方案 → KPI
                                              ↓
                                        成效追蹤
                                              ↓
                                        改進建議
                                              ↓
                                        （下一輪修正）
```

單檔 HTML（約 99KB），零外部依賴，localStorage 持久化 + JSON 匯出匯入。

---

## 這次（v1.0 → v2.0）做了什麼

### 整合遞迴自我改進
- 新增「成效追蹤」頁面（完成率、評分 1-5、經驗教訓）
- 新增「改進建議」頁面（待處理／已接受／已拒絕／已實施）
- 儀表板新增成效統計
- 簡報模式新增成效頁（共 9 頁）
- 資料模型新增 `outcomes` / `suggestions`

### 修四個實測確認的缺陷
1. **XSS** — 65 處未轉義插值。實測 `<img src=x onerror>` 會執行（`window.__XSS === 1`）。
   加 `esc()` / `num()` / `pct()` / `cls()` 四輔助函式 + CSS class 白名單。
2. **無資料遷移層** — 舊 v1.0 JSON 匯入會 `TypeError` 白畫面。加 `normalizeData()`。
3. **cascade 不完整** — 刪策略留下孤兒 KPI／成效。加 `cascadeDelete()`。
4. **`|| 0` 短路** — 吃掉真正的 0。改用 `num()`。

### 文件
README / TECH_SPEC / CHANGELOG 全部同步到 v2.0，補上資料相容性說明、
cascade 規則表、XSS 測試方法（見站內 skill 的 single-file-html-tool-lessons）。

---

## 關鍵檔案

| 檔案 | 路徑 |
|------|------|
| 工具本體 | `~/obsidian-vault/Archive/knowledge/work/strategy-blueprint-tool/index.html` |
| 資料模型 | 同目錄 `schema.json` |
| 站內頁面 | `~/web-server/projects/ai/strategy-blueprint-tool/` |
| 站內策展內容 | `~/web-server/scripts/sync-github-repos.py` 的 `REPO_CONTENT['strategy-blueprint-tool']` |

---

## 接手第一步

```bash
git clone https://github.com/share543/strategy-blueprint-tool.git
cd strategy-blueprint-tool

# 本機測試
python3 -m http.server 8000     # 開 http://localhost:8000

# 改完必跑語法檢查
python3 -c "import re,pathlib;t=pathlib.Path('index.html').read_text();open('/tmp/a.js','w').write(re.search(r'<script>(.*?)</script>',t,re.S).group(1))"
node --check /tmp/a.js
```

站內部署（改了網站內容才需要）：
```bash
cd ~/web-server
node scripts/scan-projects.mjs
/usr/bin/python3 scripts/build-list-pages.py
node scripts/check-links.mjs      # 必須 0 失敗
```

---

## 下一步（v2.1 規劃）

- [ ] **自動推導改進建議** — 從成效紀錄主動發現問題（完成率／評分過低自動產生建議草稿）
      ⚠ 動工前先定三件事：自動產生的建議可不可編輯？門檻要不要讓用戶調？
      首次使用（還沒有成效資料）該怎麼提示？
- [ ] 歷史趨勢圖表（跨期比較完成率與評分）
- [ ] 資料健康檢查（提醒未指派負責人、KPI 無時程）
- [ ] 深色/淺色主題切換
- [ ] 簡報匯出 PDF

---

## 已知未修

- `recursive-self-improvement.html` 是孤兒頁（功能已內建，規格書保留供參考，無任何地方連結它）
- localStorage 約 5MB 上限，達上限時無警告

---

## 環境陷阱

| 陷阱 | 正確寫法 |
|------|----------|
| `python3` 是 Hermes 3.14，無 PIL／jsonschema | 用 `/usr/bin/python3`，需 PIL 時加 `env -u PYTHONPATH` |
| 本機 DNS 無法解析 `share543.com` | 用 `localhost:3000` 測試 |
| GitHub Pages 更新有延遲 | push 後等 30 秒再驗 |
| `systemctl reload caddy` 在此 shell 會失敗 | `caddy reload --config ~/web-server/config/Caddyfile` |

---

## 相關 Skills

- `share543-website-management` — 站內部署流程
  - `references/single-file-html-tool-lessons.md` — **這次四個缺陷的完整修法**
  - `references/add-github-repo.md` — repo 掛上 AI 實驗頁
- `five-consultant-analysis` — 下次做整體回顧時用

---

> Built with ❤️ by share543