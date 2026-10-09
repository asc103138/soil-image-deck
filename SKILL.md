---
name: soil-image-deck
description: >
  製作 SOIL 風格全圖流 AI 簡報並自動打包為 16:9 PPTX。支援 baked 模式（圖內含字海報風）與 plate 模式（無字底圖搭配 PowerPoint 可編輯文字框）。當使用者要求「全圖簡報」、「SOIL 簡報」、「AI 生圖投影片」、「海報式簡報」、「純圖片投影片」、「視覺衝擊教學簡報」、「直播開場簡報」或「soil-image-deck」時載入此技能。
metadata:
  short-description: SOIL 全圖流 16:9 PPTX 簡報生成工作台
---

# SOIL Image Deck（Antigravity 適性版）

本技能用於製作以「全版高張力圖片」為核心的 SOIL 視覺簡報，最後將成果自動組裝為 16:9 的 PowerPoint (.pptx) 檔案。

---

## 輸出雙模式（Output Modes）

| 模式 | 特性說明 | 適用場景 |
|---|---|---|
| **`baked`（烘焙模式，預設）** | 每張圖片已由 AI 直接繪製中文標題與短句；PPTX 為每頁一張 16:9 滿版圖片。 | 高視覺衝擊、社群分享、演講開場、直播預告、不需要後續修改文字。 |
| **`plate`（底圖疊字模式）** | AI 產出乾淨無字、預留留白區的視覺底圖；PPTX 依 `spec.yaml` 疊加可編輯之 PowerPoint 文字框。 | 需保留文字修改彈性、需投影演講、長文說明、或需精確繁體中文文字排版。 |

---

## 核心生圖鐵律（Hard Image Rule）

> [!IMPORTANT]
> **本技能之每一張投影片圖片，必須優先透過 Antigravity 原生生圖工具（`generate_image`）或 `antigravity-draw` 流程產出。**
> 嚴格禁止使用本地 Pillow/Canvas/SVG 繪圖、幾何色塊或純文字排版偽裝成 AI 簡報。本技能的核心價值即在於 AI 生圖所帶來的藝術表現力與視覺張力。

---

## Antigravity 標準執行工作流程

### 1. 釐清需求與教材審查
- 確認簡報主題、受眾、預定頁數（建議 5–10 頁）。
- 若為國小/國中教材，依全域 `g4-curriculum-review` 規範落實版本對齊與三階審查。
- 決定模式：`baked` 或 `plate`。

### 2. 建立逐頁規劃（SOIL 敘事節奏）
- **引起動機（Surprise / Spark）**：封面與痛點引入，大膽配色、視覺焦點。
- **維持注意（Organize / Overcome）**：核心概念、對比、流程或關鍵數據，畫面留白清晰。
- **喚起行動（Inspire / Launch）**：總結叮嚀、行動呼籲或課堂任務。
- 每頁列出：頁碼、頁型定位、核心訊息（一句話）、畫面上文字、生圖 Prompt 摘要。

### 3. 制定視覺契約（Visual Policy）
- 色彩系統：背景深色/亮色、1-2 種主色與點綴色（如深夜藍 `#0D1B2A`、青藍 `#00C6FF`、金黃 `#FFD700`）。
- 畫面風格：扁平向量插畫 / 現代 3D 渲染 / 賽博未來 / 溫暖繪本風等。
- 統一字型規範（微軟正黑體 `Microsoft JhengHei` / 蘋方 `PingFang TC`）。

### 4. 逐頁調用 Antigravity 原生生圖工具
調用 `generate_image` 工具：
- `AspectRatio`: `'16:9'`（投影片標準比例）。
- `ImageName`: `page_01`, `page_02`, ...
- `Prompt`: 依 `references/image-prompts.md` 指引構建結構化提示詞。
- 產出後將圖片依序存放於專案 `slides/images/page_01.png`、`page_02.png` 等。

### 5. 視覺檢查與 QA
- 檢查圖片比例（16:9）、清晰度與風格一致性。
- `baked` 模式：檢查畫面中文字是否正確無錯別字、字數是否在 20 字以內。
- `plate` 模式：檢查底圖是否保持乾淨、文字預留區是否留白足夠。

### 6. 打包成 PPTX
在終端機執行打包腳本（支援 `uv` 或專案虛擬環境）：

#### 烘焙模式 (`baked`)：
```bash
python scripts/pack_pptx.py \
  --images-dir slides/images \
  --output slides/output.pptx \
  --mode baked
```
或使用 `uv` 隨選執行：
```bash
uv run --with python-pptx --with Pillow --with PyYAML python scripts/pack_pptx.py \
  --images-dir slides/images \
  --output slides/output.pptx \
  --mode baked
```

#### 底圖疊字模式 (`plate`)：
```bash
python scripts/pack_pptx.py \
  --images-dir slides/images \
  --output slides/output-editable.pptx \
  --mode plate \
  --spec slides/spec.yaml
```

### 7. 驗證與交付成果
- 回報生成的 `.pptx` 絕對路徑與投影片頁數。
- 提供成果截圖或投影建議。

---

## 設計細則（Design Rules）

1. **一頁一重點**：每張投影片只聚焦傳達單一概念。
2. **Baked 字數上限**：烘焙模式中文字盡量在 20 字以內，避免 AI 產生亂碼或字體崩壞。
3. **Plate 精確座標**：以 16:9 畫布（寬 13.333 英吋 × 高 7.5 英吋）為基準，參考林長揚海報比例（標題 72/55pt、副標 34pt、內文 21pt）。
4. **色彩對比**：深底淺字或淺底深字，文字區保持足夠明暗對比。

---

## 參考文件與規範

- `references/spec-format.md`：`plate` 模式之 `spec.yaml` 格式與元件清單（title, subtitle, badge, card, bar, progress）。
- `references/image-prompts.md`：AI 生圖提示詞撰寫範本與負向提示詞。

---

## 依賴套件

- Python 套件：`python-pptx`, `Pillow`, `PyYAML`。
- 本機環境：macOS 原生 zsh、Python 3.10+、`uv`。
