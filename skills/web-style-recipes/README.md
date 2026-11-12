# web-style-recipes

實驗型互動首頁的風格配方庫——一個 [Claude Code](https://claude.com/claude-code) Agent Skill。

做作品集、活動頁、產品首頁時，不想要罐頭模板感，又不想每次從「幫我做個有質感的網頁」這種空話開始？這份 skill 把風格拆成**看得見的元素**：視覺特徵清單、一句話流程、迭代順序、技術陷阱、可直接貼的 prompt，和給 Claude Design 用的 brief 卡。

## 內容

**11 種互動配方**（`references/styles/`）——每種是一個完整做法：

| # | 配方 | # | 配方 |
|---|---|---|---|
| 01 | 復古自拍亭／拍貼機 | 07 | 電子郵票 |
| 02 | 熱感應／熱像儀 | 08 | 動態文字 |
| 03 | 音檔可視化／聲紋 | 09 | 像素房間 |
| 04 | 白板便利貼 | 10 | 重力感應 |
| 05 | CCTV 監控畫面 | 11 | Hairline 等距線稿 |
| 06 | 萬花筒 | | |

**20 種美學風格**（`references/aesthetics.md`）——每種是一種視覺語言的骨架（從哪來、美在哪、給 AI 的一條規則），分四組：平面與印刷（瑞士、Riso、紙張拼貼、包浩斯、孟菲斯、線條畫）、動態與電影（動態文字、普普、合成波、故障風、蒸氣波）、3D 與材質（黏土、毛玻璃、Y2K 鉻、粒子、低多邊形）、介面與遊戲（扁平 2D、新粗獷、像素風、等距視角）。

配方和美學可以疊：像素房間配方＋像素風的陰影規則、動態文字配方＋ Saul Bass 的節拍規則。

**探索模式**（`references/explore.md`）——還沒定方向時先發散再收斂：3–4 個方向並排比稿 → 同方向 5 個變體（每個只改一個維度）→ 才開工。

## 安裝

```bash
git clone https://github.com/lu791019/web-style-recipes.git ~/web-style-recipes
ln -s ~/web-style-recipes ~/.claude/skills/web-style-recipes
```

開新的 Claude Code session 後生效。

## 用法

| 說法 | 效果 |
|---|---|
| 「做一個熱感應風格的首頁」 | 自動載入對應配方開工 |
| `/web-style-recipes` | 選單：先選分類，再選風格 |
| `/web-style-recipes 02` 或 `熱感應` | 直接指定配方 |
| `/web-style-recipes 美學` 或 `包浩斯`、`A09` | 美學風格庫 |
| `/web-style-recipes 探索` | 發散比稿模式 |
| 任一用法＋「只要 brief」 | 不寫程式，只出可貼進 Claude Design 的 brief 卡 |

## 核心原則

1. 特徵要看得見：用「深紅絨布簾」而不是「復古感」。
2. 流程就是驗收標準：一句話流程的每個箭頭都要有畫面回饋。
3. 一次只改一件事。
4. 可讀與舒適優先於炫：主標有 DOM 文字、尊重 reduced-motion、權限被拒不會壞。
5. 開頁就有畫面。
6. 先說出處再動手：做任何畫面前先講參考哪一件經典（作者、作品、年份）。AI 沒被告知什麼叫美，就會給平均值。

## 結構

```
SKILL.md                  ← 入口：索引表、用法、開工流程
references/
  method.md               ← 五段式方法＋brief 卡模板
  pitfalls.md             ← 共通技術陷阱（getUserMedia、Canvas 跨來源、reduced-motion…）
  aesthetics.md           ← 20 種美學風格（每種附出處與記憶卡）
  explore.md              ← 探索模式流程
  styles/01-*.md … 11-*.md ← 每個配方一檔，欄位固定
tests/                    ← 實測產物（HTML＋手機/桌機截圖）
```

新增風格：加一個 `references/styles/NN-名稱.md`（欄位照既有檔案），更新 SKILL.md 索引表；實測撞到新陷阱回寫到該風格檔或 `pitfalls.md`。

## 出處

- 11 種配方的題材靈感來自 AI郵報〈[【AI 工具地圖】ChatGPT、Claude 也能這樣玩！10 種 Vibe Coding 網站設計靈感](https://www.aiposthub.com/vibe-coding-website-ideas/)〉（Joanna Chang，2026-10）。原文未附轉載授權，故**本庫全部內容為自行重寫**：特徵、流程、陷阱、prompt 皆為自己的結構與用語，僅題材同源並註明出處。
- 20 種美學風格每種都在 `aesthetics.md` 檔內註明源流（運動、代表人物、年代）。
