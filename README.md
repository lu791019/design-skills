# design-skills

三支前端設計用的 Claude Code Agent Skills，整理成一包，方便一次安裝。

| Skill | 用途 | 來源 | 授權 |
|---|---|---|---|
| `ui-ux-pro-max` | UI/UX 設計資料庫：80 種風格、192 組配色、74 組字型搭配、120 條 UX 準則、圖示、GSAP 預設、圖表類型、22 種技術棧，附本機搜尋腳本 | [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | MIT |
| `impeccable` 4.8.2 | 設計、重設計、審查、打磨、加動畫：網站、Landing page、Dashboard、App UI、元件、設計系統（DESIGN.md）。含 `/impeccable audit`、`polish`、`animate` 等子命令 | [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | Apache-2.0 |
| `web-style-recipes` | 實驗型互動首頁風格配方 11 種（拍貼機、熱像、聲紋、CCTV、萬花筒、像素房間、重力感應…）＋ 20 種有出處的美學風格（瑞士、包浩斯、孟菲斯、Riso、蒸氣波、新粗獷…），可只出給 Claude Design 的 brief 卡 | [lu791019/web-style-recipes](https://github.com/lu791019/web-style-recipes) | 見該 repo |

## 安裝

用 [skills CLI](https://github.com/vercel-labs/skills)，一次裝三支：

```bash
npx skills add lu791019/design-skills
```

只裝其中一支：

```bash
npx skills add lu791019/design-skills --skill web-style-recipes
```

或手動 clone 後把各 skill 目錄接到 `~/.claude/skills/`：

```bash
git clone https://github.com/lu791019/design-skills.git ~/design-skills
for s in ui-ux-pro-max impeccable web-style-recipes; do
  ln -s ~/design-skills/skills/$s ~/.claude/skills/$s
done
```

開新的 Claude Code session 後生效。`impeccable` 的 `scripts/impeccable` 啟動器第一次執行時會從 GitHub Releases 下載對應平台的引擎二進位並核對 `engine-checksums.txt`。

## 用法

| 說法 | 進哪支 |
|---|---|
| 「幫我選這個 SaaS 的配色和字型」「檢查這頁的無障礙」 | ui-ux-pro-max |
| `/impeccable audit`、`/impeccable polish src/App.tsx`、「把這個 dashboard 重設計」 | impeccable |
| 「做一個熱感應風格的首頁」、`/web-style-recipes 包浩斯`、「只要 brief」 | web-style-recipes |

三支可以疊：先用 web-style-recipes 定風格方向，ui-ux-pro-max 查配色字型，最後用 impeccable 審查與打磨。

## 結構

```
skills/
  ui-ux-pro-max/      SKILL.md、data/（CSV 資料庫）、scripts/search.py、references/、LICENSE
  impeccable/         SKILL.md、reference/、scripts/、LICENSE、NOTICE.md
  web-style-recipes/  SKILL.md、README.md、references/、tests/（實測截圖）
```

## 授權與出處

- `ui-ux-pro-max`：MIT，© Next Level Builder，原文照搬，LICENSE 在該目錄。
- `impeccable`：Apache-2.0，© Paul Bakaus，取自上游 `plugin/skills/impeccable`，LICENSE 與 NOTICE.md 在該目錄。
- `web-style-recipes`：Dex（lu791019）撰寫；11 種配方題材出處與 20 種美學風格的源流都寫在該 skill 的 README 與 `references/aesthetics.md`。
