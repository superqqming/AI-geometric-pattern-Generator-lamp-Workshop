# 簡易版模擬器 — 學員 60 分鐘實作指南

> 用 Claude Code 從零做出一個能跑的 lamp pattern simulator。
> 完成後對照完整版、理解每個進階功能解決什麼問題。

---

## 你會做出什麼

一個 `lamp-studio.html`（約 100-150 行）、可以：
- 上傳圖片
- 滑桿調整黑白閾值
- 一鍵向量化
- 一鍵下載 DXF 給雷切機

**刻意不做**（完整版才有、之後對照學）：
- Flood-fill 把線稿轉成孔洞
- 自動描外輪廓
- 中央機構淨空
- 輻射支撐
- AI 生圖（用網頁版 ChatGPT/Gemini 代替）

---

## 開始之前

1. 確認 Claude Code 能在 terminal 跑（打 `claude` 啟動）
2. 桌面建一個資料夾：`my-lamp-studio/`
3. `cd` 進去、啟動 Claude Code
4. 開瀏覽器分頁、準備一張黑白線稿（搜尋 "geometric pattern line art" 隨便存一張）

---

## 階段一（10 分鐘）— 上傳圖、預覽顯示

**目標**：開 HTML、上傳圖、圖出現在 canvas 上。

**貼給 Claude Code**：
```
我要做一個網頁工具、可以上傳圖片然後輸出 DXF 給雷切機用。
先做第一步：建立 lamp-studio.html、裡面要有：

- 一個檔案上傳按鈕（type="file" accept="image/*"）
- 一個 800x800 的 canvas
- 上傳後把圖片畫到 canvas 上（用 drawImage、自動縮放到 contain）

一個 .html 檔搞定、CSS 跟 JS 都內嵌。深色背景、白字、簡潔就好。
```

**完成樣子**：點上傳、選一張圖、canvas 顯示出來。

---

## 階段二（15 分鐘）— 閾值滑桿、即時黑白化

**目標**：拖滑桿時、canvas 即時變成純黑白二值圖。

**貼給 Claude Code**：
```
接下來：
- 在 canvas 下方加一條滑桿（min=0、max=255、預設 128）、旁邊顯示數值
- 拖動時、用 getImageData 取出 canvas、每個像素：
  灰階值 (0.299*R + 0.587*G + 0.114*B) 大於閾值 → 白、小於 → 黑
- 寫回 canvas、即時更新

要注意：每次拖滑桿要重畫原圖再做 threshold、不然會越調越黑。
```

**完成樣子**：滑桿低 → 圖大部分變黑、滑桿高 → 大部分變白、中間值看到清楚的黑白線稿。

**教學重點**：threshold 就是「把灰階世界切成兩個顏色」的最簡單方法。

---

## 階段三（20 分鐘）— 向量化

**目標**：按按鈕、把黑白圖追蹤成線條、疊在 canvas 上看。

**貼給 Claude Code**：
```
加向量化功能：
- <head> 裡引入 ImageTracer.js：
  <script src="https://cdn.jsdelivr.net/gh/jankovicsandras/imagetracerjs/imagetracer_v1.2.6.js"></script>
- 加「向量化」按鈕
- 按下後：
  1. 從 canvas 取 ImageData
  2. 呼叫 ImageTracer.imagedataToTracedata(data, { numberofcolors: 2, pathomit: 8 })
  3. 抓出黑色那層（palette 亮度 < 128）的所有 path
  4. 用 SVG 元素覆蓋在 canvas 上方、把每條 path 畫成黃色線
  5. 顯示「找到 N 條路徑」

存路徑到 window.tracedPaths 變數、待會輸出 DXF 用。
```

**完成樣子**：按下後 canvas 上出現黃色線條描出圖形輪廓、下方寫「找到 X 條路徑」。

**教學重點**：點陣（pixel grid）→ 向量（數學上的線段）。雷切機只認向量、不認 pixel。

---

## 階段四（15 分鐘）— 輸出 DXF

**目標**：把向量路徑包成 DXF 檔下載。

**貼給 Claude Code**：
```
最後加「下載 DXF」按鈕：

DXF 是雷切機讀的純文字 ASCII 格式。最小可用結構：

0
SECTION
2
ENTITIES
0
POLYLINE
8
PATTERN
66
1
70
1
0
VERTEX
8
PATTERN
10
<x>
20
<y>
30
0
（每個點一組 VERTEX）
0
SEQEND
（每條路徑一組 POLYLINE...SEQEND）
0
ENDSEC
0
EOF

要做的事：
- 從 window.tracedPaths 讀每條路徑
- 翻轉 Y 軸（DXF 的 Y 朝上、canvas 朝下、用 canvas_height - y）
- 把每條路徑包成一個 POLYLINE block
- 用 Blob + URL.createObjectURL + a.download 觸發下載
- 檔名 lamp-pattern.dxf

縮放：canvas 是 800px、實際輸出當作 90mm（除以 8.89 換算）。
```

**完成樣子**：按下載、得到 `lamp-pattern.dxf`。用 LibreCAD（免費）或線上 DXF viewer 打開、看到線條對得上。

**教學重點**：DXF 看起來很複雜、其實只是「一行 code、一行值」的文字檔。1980 年代的標準、所有 CAD 都吃。

---

## 完成檢查表

打開 `lamp-studio.html`、跑一遍：

- [ ] 上傳一張黑白線稿
- [ ] 圖出現在 canvas
- [ ] 拖閾值滑桿、看到黑白比例變化
- [ ] 停在線條清楚的位置
- [ ] 按「向量化」、看到黃色路徑覆蓋
- [ ] 按「下載 DXF」、得到檔案
- [ ] DXF 拖進 LibreCAD（或 https://sharecad.org 線上預覽）、線條對得上

七項全勾 = 完成。

---

## 對照完整版、你少了什麼？

打開 `lamp-pattern-studio.html`（老師提供的完整版）對照：

| 你的簡易版 | 完整版多了 | 解決什麼問題 |
|---|---|---|
| 線條直接變切割路徑 | Flood-fill 把線稿轉成「封閉孔洞」 | 防止切下來散成碎片 |
| 沒有外輪廓 | 自動描 lamp piece 真實外形 | DXF 能切出整個零件 |
| 沒有機構孔 | 2 個 3×3mm 固定孔可調 | 對應實際燈具安裝位置 |
| 沒有淨空區 | 中央 keepout 圓擦掉孔 | 給轉接結構靠合 |
| 沒有結構強化 | 輻射支撐 spoke 可選 | 處理同心圓 pattern |
| 只有 threshold | + 模糊 + 形態學 + 簡化 | 處理不同來源的圖片品質 |
| 固定 canvas 大小 | W×H bounding box 可調 | 燈具支援多種尺寸 |

**每一項都是把「AI 生的圖」變成「能裝上燈具的零件」的必要橋梁。**

---

## 卡住時的求救句

跟 Claude Code 描述狀況、它幾乎都能修：

- **看到錯誤**：「我看到這個錯誤訊息：[貼 console 訊息]、怎麼修？」
- **沒反應**：「我按按鈕但沒任何反應、幫我加 console.log 找出問題」
- **結果不對**：「我希望看到 X、但實際看到 Y、可能是哪裡？」
- **完全迷路**：「我跟丟了、目前 lamp-studio.html 的狀態是這樣：[貼整個檔案]、下一步要做 [貼指南那段]」

---

## 為什麼這樣設計？

這個簡易版**刻意省略**所有「機構限制」相關的東西、純粹是 pixel → vector → DXF 的最小管線。

省略的東西不是因為不重要、而是因為**它們才是這堂課的真正核心**。讓你先親手做一遍「沒考慮限制」的版本、之後看完整版才會懂：

> 那些多出來的步驟、是為了「讓 AI 想出來的東西、能真的被機器做出來」。

這就是「AI × 機構限制」這堂課的論述。
