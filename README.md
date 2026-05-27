# AI × 機構限制 — 燈具 Pattern 工作坊

> 用 AI 生成圖像、自動轉換為符合燈具機構限制的雷切 DXF 檔。
> 不用 CAD、不用寫 code、也能做出能直接製造的 pattern 板。

---

## 🚀 立即開始（工具）

| 工具 | 連結 | 用途 |
|---|---|---|
| 🪔 主模擬器 | [lamp-pattern-studio.html](https://superqqming.github.io/AI-geometric-pattern-Generator-lamp-Workshop/lamp-pattern-studio.html) | AI 生圖 / 上傳圖 → 雷切 DXF |
| 📐 排版工具 | [nesting-tool.html](https://superqqming.github.io/AI-geometric-pattern-Generator-lamp-Workshop/nesting-tool.html) | DXF → 390×297 板材最佳排版 |

---

## 📖 學員必讀

| 文件 | 內容 |
|---|---|
| [📘 使用指南 student-user-guide.md](./student-user-guide.md) | 模擬器 UI 怎麼用、三條創作路徑、常見問題 |
| [🤖 AI 提示詞範本 student-ai-prompts.md](./student-ai-prompts.md) | 給 ChatGPT/Gemini 的提示詞、自我檢查清單、搜尋關鍵字 |

---

## 📚 想深入了解

| 文件 | 內容 |
|---|---|
| [🏛️ 系統開發架構 architecture.md](./architecture.md) | 整個模擬器怎麼運作、AI 介入點在哪、為什麼這樣設計 |
| [🛠️ 選擇性：自己做簡易版 student-build-guide.md](./student-build-guide.md) | 60 分鐘用 Claude Code 做出自己的簡化版（需要 Claude Code 環境、進階學員選讀） |

---

## 🎓 課程主軸

> **AI 可以生出無限漂亮的圖、但能不能變成「能被機器做出來」的東西？**

這個工具示範中間那道「翻譯」：

```
AI 生圖（隨意創作）
    ↓
程式碼自動消化：
  • 封閉細胞偵測（flood-fill）
  • 外輪廓追蹤（envelope tracing）
  • 中央機構淨空
  • 結構連通驗證
    ↓
輸出 DXF → 雷切機讀得懂
```

學員體會的是：**限制不是壓抑創意、是讓創意能落地**。

---

## 🛠️ Tech Stack

- 純 HTML / JavaScript（單一 `.html` 檔、瀏覽器直接打開）
- [ImageTracer.js](https://github.com/jankovicsandras/imagetracerjs) — 點陣轉向量
- Cloudflare Worker — API 代理（藏 API key）
- Anthropic Claude (`claude-haiku-4-5`) — 中文描述改寫
- OpenAI `gpt-image-1` — 圖像生成

---

*Anature Life Lab Workshop · 2026*
