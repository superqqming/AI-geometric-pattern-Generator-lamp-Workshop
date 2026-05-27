# 🤖 給學員的 AI 圖像生成提示詞

> 兩個情境、兩套提示詞、複製貼到 ChatGPT / Gemini / Copilot 都可以用。

---

## 情境 1：純文字 → 圖（最常用）

你有想要的意象、但沒素材時用這個。

打開 [ChatGPT](https://chat.openai.com) 或 [Gemini](https://gemini.google.com)、貼下面這段、把 `[主題]` 換成你想要的：

```text
Generate a black and white geometric line-art image suitable for laser cutting.

主題 Subject: [這裡填你想要的、例如「water ripples 水波」「honeycomb 蜂巢」
             「mandala 曼陀羅」「islamic tile 伊斯蘭瓷磚」「botanical mesh 植物網」]

STYLE — 必須遵守:
- Pure black lines on pure white background
- Single uniform line weight (about 2-3 px in a 1024x1024 image)
- High contrast monochrome — NO shading, NO gradients, NO fill colors
- Vector illustration / clean line drawing style
- Centered composition, fills about 80% of the image area

STRUCTURE — 結構鐵則（切下來不能散）:
- All lines must INTERSECT and CONNECT — form a single connected mesh
- NO isolated rings, NO pure concentric circles without radial dividers
- If using concentric structure, ADD radial spokes crossing all layers
- Reference: Islamic geometry, mandala with radial spokes, Voronoi cells,
  hexagonal tessellation, branching botanical mesh
- Each enclosed cell should be small-to-medium sized

OUTPUT: 1024x1024 square image, downloadable as PNG.
```

---

## 情境 2：上傳參考圖 → AI 重新繪製

你在網路上找到一張看起來不錯但不能直接用的圖（例如有顏色、陰影、線條太細）、想讓 AI 幫你重做成乾淨的線稿。

**先上傳圖、再貼以下提示詞**：

```text
我會上傳一張參考圖、請你幫我**重新繪製**一張雷切可用的黑白線稿、
最後輸出一張 1024×1024 的圖片給我下載。

# 從參考圖中擷取
- 看一下這張圖、找出它的「幾何核心結構」
  （例如：六角網格、放射對稱、編織、Voronoi 細胞、伊斯蘭鋪磚等）
- 不要照搬細節、只取結構與意象、轉成純線條版本

# 風格規格 (mandatory)
- Pure black lines on pure white background
- Single uniform line weight (約 2-3 px in 1024×1024 image)
- High contrast monochrome — NO shading, NO gradients, NO fill colors
- Vector illustration / clean line drawing style
- Centered composition, fills about 80% of the image area

# 結構鐵則 (so it doesn't fall apart when laser cut)
- 所有線條必須 INTERSECT and CONNECT、形成單一連接的網狀結構
- 禁止：純同心圓、純同心橢圓、孤立的環、分散不接觸的形狀
- 如果原圖有同心圓結構、必須加上 radial spokes 穿透所有環、讓內外連通
- 每個封閉細胞大小適中（不要一大塊空白、也不要 1mm 以下太細的格子）

# 輸出
1024×1024 PNG、純黑白、可下載
```

---

## 哪個 AI 工具可以用？

| 工具 | 文字 → 圖 | 圖片 → 重畫 | 備註 |
|---|---|---|---|
| **ChatGPT**（有 DALL-E） | ✅ | ✅ | 最穩、免費版即可 |
| **Google Gemini** | ✅ | ✅ | 免費版可用 |
| **Microsoft Copilot** | ✅ | ⚠️ | 部分版本支援 |
| **Bing Image Creator** | ✅ | ❌ | 只能純文字 |
| **Claude 網頁版** | ❌ | ❌ | Claude 本身不生圖、不適用 |

---

## ✅ 自我檢查清單

生成後肉眼快速看一遍：

- [ ] **純黑白？** 沒有灰階、藍色、綠色
- [ ] **背景純白？** 不是米白也不是淡灰
- [ ] **線條粗細一致？** 沒有有的地方粗、有的地方細到看不見
- [ ] **有封閉的小區塊？** 不是斷掉的線、要看得到「格子」
- [ ] **線條有交叉？** 不是一堆獨立圓圈疊在一起

任一項沒過 → 把問題寫出來、叫 AI 改、例如：

- 「線條太細、請再加粗一倍」
- 「有同心圓沒交叉、請加上放射狀的線連接內外圈」
- 「背景不是純白、有淡淡紋理、請改成純白」
- 「請降低細節密度、有些格子太小（小於 5mm）」
- 「圖太偏一邊、請置中」

---

## 找參考圖的搜尋關鍵字（給 Google 圖片）

| 想要的風格 | Google 搜尋 |
|---|---|
| 蜂巢 / 規律幾何 | `hexagonal tiling pattern`、`hexagon line drawing` |
| 曼陀羅 / 放射 | `mandala line art`、`mandala outline pattern` |
| 伊斯蘭幾何 | `islamic geometric pattern`、`moroccan tile line` |
| 自然紋理 | `botanical line art`、`leaf vein pattern` |
| 染色玻璃 | `stained glass pattern line drawing` |
| 街道 / 鋪面 | `pavement pattern geometric`、`brick pattern` |
| 編織 / 結繩 | `celtic knot pattern`、`woven pattern line` |

加上 `line art`、`black and white`、`outline` 結果會更接近可用形式（AI 重畫的工作量也比較少）。

---

## 一個 AI 寫不好的地方：同心圓

AI 很愛生「靠輻射 / 純同心圓」的圖、但雷切後同心圓會把片切成多塊、無法使用。

如果生出來真的是純同心圓、**換個關鍵字重生**比硬要 AI 修還快：

| ❌ 避免 | ✅ 改用 |
|---|---|
| spiral | woven spiral with cross dividers |
| concentric circles | rings divided by radial spokes |
| ripples | rippling waves intersected by radial lines |
| target / bullseye | radial mandala with intersecting layers |

---

## 完成之後

下載 PNG → 打開 [模擬器](https://superqqming.github.io/AI-geometric-pattern-Generator-lamp-Workshop/lamp-pattern-studio.html) → 走「📤 上傳圖片」路徑 → 輸出 DXF。

詳細模擬器操作請看 [使用指南 student-user-guide.md](./student-user-guide.md)。
