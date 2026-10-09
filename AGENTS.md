# soil-image-deck - AGENTS.md

## 專案資訊
- **專案名稱**：SOIL 全圖流 AI 簡報生成工作台 (soil-image-deck)
- **專案用途**：使用 Antigravity 原生生圖（`generate_image`）與 PPTX 打包腳本，自動產出 16:9 高張力視覺簡報（支援 baked 圖文海報模式與 plate 底圖疊字模式）。
- **主要工作目錄**：`/Users/tunyuan/anti/soil-image-deck`
- **全域技能路徑**：`~/.gemini/config/skills/soil-image-deck`
- **GitHub Repo**：https://github.com/asc103138/soil-image-deck

## Obsidian 關聯筆記
- **Vault 路徑**：`/Users/tunyuan/opencode_0715`
- **專案駕駛艙**：`/Users/tunyuan/opencode_0715/04-專案/soil-image-deck-專案駕駛艙.md`

## 工作與安全規則
- 回應使用繁體中文（台灣）。
- 開工時讀本檔、讀 Obsidian 駕駛艙、檢查 Git 狀態。
- 收工時更新 Obsidian 駕駛艙，檢查 diff 後精準 stage 相關檔案，嚴格禁止 `git add .`。
- 絕不 commit API Key、Token、密碼或個人隱私資料。
- 學生資料僅記錄班級代號與座號，不儲存真名。
- **全域教材審查規範**：凡涉及生成國中小考卷、學習單、教學簡報或教材，必須嚴格落實 `g4-curriculum-review` 三階審查（第一階課綱版本門檻、第二階 CLT 認知負荷與退回確認、第三階迷思診斷與海線在地化），通過自我檢測並隨附審查報告後始得輸出交付。
- **生圖鐵律**：投影片視覺核心必須由 Antigravity 原生生圖能力（`generate_image`）或 `antigravity-draw` 產出，嚴禁使用本地 Pillow/SVG/HTML 繪圖取代。
