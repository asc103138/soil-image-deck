# Plate 模式 YAML 規格書規範（Spec Format Guide）

當使用 `plate` 模式時，由 AI 產出乾淨無字視覺底圖，並使用 `slides/spec.yaml` 定義 PowerPoint 內的可編輯文字框與視覺元件。

---

## 範例規格檔（`spec.yaml`）

```yaml
style:
  palette:
    bg: "#0D1B2A"
    primary: "#00C6FF"
    highlight: "#FFD700"
    text: "#FFFFFF"
    muted: "#A5B4CB"
    card: "#1E3A5F"
  # 支援跨平台字型名稱：微軟正黑體、蘋方、思源黑體
  font: "Microsoft JhengHei"
  title_font: "Microsoft JhengHei"
  body_font: "Microsoft JhengHei"

pages:
  - page: 1
    image: page_01
    img_x: 0
    img_y: 0
    img_w: 13.333
    img_h: 7.5
    bg: bg
    blocks:
      - type: badge
        text: "EP15"
        x: 0.7
        y: 0.7
        w: 2.2
        h: 0.5
        bg: primary
        color: bg
        size: 14
      - type: title
        text: "把生圖\n放進簡報"
        x: 0.7
        y: 1.6
        w: 6.5
        h: 2.5
        size: 48
        color: text
        bold: true
      - type: subtitle
        text: "Antigravity × SOIL 投影片工作流"
        x: 0.7
        y: 4.75
        w: 6.5
        h: 1
        size: 22
        color: primary
      - type: progress
        current: 1
        total: 5
        x: 0.7
        y: 6.8
        w: 4.0
        h: 0.08
        track: card
        color: primary
```

---

## 元件類型（Block Types）

| 類型 (type) | 說明 | 關鍵屬性 |
|---|---|---|
| `title` | 大標題（預設 72pt、粗體） | `text`, `x`, `y`, `w`, `h`, `size`, `color`, `bold`, `align` |
| `subtitle` | 副標題（預設 34pt、主色） | `text`, `x`, `y`, `w`, `h`, `size`, `color` |
| `body` | 內文段落（預設 21pt、行距 1.2） | `text`, `x`, `y`, `w`, `h`, `size`, `line_spacing` |
| `badge` | 膠囊型標籤（圓角色塊 + 置中文字） | `text`, `bg`, `color`, `size` |
| `card` | 圓角視覺背景卡片（無文字） | `bg`, `border`, `border_width` |
| `bar` | 細裝飾分隔線 | `x`, `y`, `w`, `h`, `color` |
| `progress` | 投影片進度條（減輕觀眾心理負擔） | `current`, `total`, `track`, `color` |
| `highlight` | 強調醒目字（預設 26pt、高亮金黃） | `text`, `size`, `color` |
| `muted` | 註腳或次要提示（預設 14pt、灰藍） | `text`, `size`, `color` |

---

## 畫布座標基準（Canvas Metrics）

- 投影片比例為標準 16:9，對應 PowerPoint 實體尺寸：**寬 13.333 英吋 × 高 7.5 英吋**。
- 座標系 `(x, y)` 以投影片左上角為原點 `(0, 0)`，單位皆為英吋（Inches）。
