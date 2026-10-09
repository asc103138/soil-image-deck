# SOIL Image Deck（全圖流 AI 簡報工作台）

> **專為 Antigravity 適性化打造之全圖流 16:9 AI 簡報生成工作台**  
> 結合 Antigravity 原生生圖工具（`generate_image`）與 Python PPTX 高保真打包引擎，快速製作極具視覺張力的全圖簡報。

---

## 🌟 核心特色

1. **SOIL 節奏敘事架構**：引起動機（Spark） ➔ 維持注意（Organize） ➔ 喚起行動（Inspire）。
2. **雙輸出模式支援**：
   - **`baked` 烘焙模式**：AI 直接在圖中生成醒目中文標題與金句（字數 ≤ 20 字），打包為 16:9 滿版高張力海報投影片。
   - **`plate` 底圖疊字模式**：AI 生成乾淨無字且預留文字區的視覺底圖，透過 `spec.yaml` 疊加可編輯之 PowerPoint 向量文字框與元件。
3. **Antigravity 原生適性**：
   - 全面整合 Antigravity 原生生圖工具（無需外接任何外部付費 API）。
   - 提供 macOS 原生 zsh CLI、Python 虛擬環境與 `uv` 隨選執行支援。
   - 相容微軟正黑體、蘋方（PingFang TC）等繁體中文字型。

---

## 📁 專案架構

```text
soil-image-deck/
├── SKILL.md                  # Antigravity 技能定義檔
├── AGENTS.md                 # 專案規則與安全指引
├── ANTIGRAVITY.md            # Antigravity 專案入口引導
├── README.md                 # 專案說明文件
├── requirements.txt          # Python 依賴清單
├── .gitignore                # Git 忽略設定
├── references/
│   ├── image-prompts.md      # AI 生圖提示詞指南與負向約束
│   └── spec-format.md        # Plate 模式 YAML 規格書指南
├── scripts/
│   └── pack_pptx.py          # PPTX 打包引擎（支援 baked 與 plate 雙模式）
└── slides/
    ├── images/               # 存放生成的投影片圖片（page_01.png, page_02.png...）
    └── spec.yaml             # Plate 模式規格範本
```

---

## 🛠️ 環境配置與依賴安裝

本專案支援使用 `uv` 快速配置虛擬環境：

```bash
# 建立虛擬環境並安裝依賴
uv venv .venv
uv pip install -r requirements.txt --python .venv/bin/python
```

或使用全域 `uv run` 免安裝直接執行：
```bash
uv run --with python-pptx --with Pillow --with PyYAML python scripts/pack_pptx.py --help
```

---

## 🚀 打包指令

### 1. 烘焙模式（Baked Mode，預設）
將 `slides/images/` 目錄下的所有投影片圖片打包為滿版 16:9 PPTX：

```bash
.venv/bin/python scripts/pack_pptx.py \
  --images-dir slides/images \
  --output slides/output.pptx \
  --mode baked
```

### 2. 底圖疊字模式（Plate Mode，可編輯文字）
依 `slides/spec.yaml` 定義將無字底圖與文字方塊組合成可編輯之 16:9 PPTX：

```bash
.venv/bin/python scripts/pack_pptx.py \
  --images-dir slides/images \
  --output slides/output-editable.pptx \
  --mode plate \
  --spec slides/spec.yaml
```

---

## 💡 Antigravity 對話使用流程

在 Antigravity 對話中，你可以直接這樣跟 Agent 說：

1. **規劃階段**：
   > 「我想做一份關於『國小四年級分數概念』的 5 頁 SOIL 全圖簡報，使用 baked 模式。」
2. **生圖階段**：
   > Agent 會自動呼叫 `generate_image` 工具（設定 `AspectRatio: '16:9'`），逐頁產出高畫質投影片圖片並存放至 `slides/images/`。
3. **打包階段**：
   > Agent 自動執行 `pack_pptx.py` 打包成可下載或播放的 `.pptx` 簡報。

---

## 📖 相關文件

- [SKILL.md](file:///Users/tunyuan/anti/soil-image-deck/SKILL.md)
- [image-prompts.md](file:///Users/tunyuan/anti/soil-image-deck/references/image-prompts.md)
- [spec-format.md](file:///Users/tunyuan/anti/soil-image-deck/references/spec-format.md)
- [Obsidian 專案駕駛艙](file:///Users/tunyuan/opencode_0715/04-專案/soil-image-deck-專案駕駛艙.md)
