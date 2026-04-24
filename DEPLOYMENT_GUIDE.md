# Fellowship Planner — Deployment Guide

**工具名稱:** 團契週會設計器 · Fellowship Meeting Planner
**版本:** v1.0
**作者:** Ivan Hui (串嘴大叔)
**最後更新:** 2026-04-24
**架構:** 純前端單一 HTML 檔 (52KB, 零依賴, 零 API)

---

## §1 呢個 Tool 係乜?

一個**靜態網頁表單 + Prompt 生成器**,幫團契/小組同工設計週會活動。

- 用戶喺網頁填表(55 個欄位,大部分選填)
- 按「生成 Prompt」,網頁會組裝一段完整嘅結構化 prompt
- 用戶 copy,貼去佢自己嘅 AI(ChatGPT / Claude / Gemini)
- **零 API 成本**(你唔駛俾錢)、**零後端**(唔駛 server)、**零收集**(完全 client-side)

---

## §2 部署前準備

### 需要嘅嘢

| 項目 | 係咪一定要 | 備註 |
|---|---|---|
| GitHub 帳號 | ✓ 必須 | 用免費 GitHub Pages |
| `fellowship-planner.html` 檔案 | ✓ 必須 | 已經俾你 |
| 網域(custom domain) | ✗ 選擇性 | 用 `*.github.io` 已經夠 |
| 本地編輯器 | ✗ 選擇性 | 喺 GitHub 網頁直接編輯都可以 |

### 選擇部署路線

**Route A:** 整個新 repo 專門放呢個 tool(最簡單)
**Route B:** 加入你現有嘅 `ivantheservant.github.io` repo(整合現有生態)
**Route C:** 整個 ministry-tools hub,將來放埋兒主 generator 一齊(長遠最好)

以下每條路線都有步驟。

---

## §3 Route A — 新 Repo 單獨部署

**最快,10 分鐘搞掂。適合第一次試。**

### 步驟

1. **登入 GitHub** → 右上角 `+` → `New repository`
2. **Repo 名:** 建議 `fellowship-planner`(或你鍾意嘅名)
3. **Visibility:** Public(Pages 免費版只支援 Public)
4. **勾 Add a README file** → `Create repository`
5. 入到 repo,click `Add file` → `Upload files`
6. 將 `fellowship-planner.html` **改名為 `index.html`**,然後 upload
7. Click `Commit changes`
8. 入 `Settings` → 左邊 `Pages`
9. **Source:** Deploy from a branch
10. **Branch:** `main` / `root` → `Save`
11. 等 1-3 分鐘,頂部會出現網址:`https://{你嘅username}.github.io/fellowship-planner/`

### 驗證

- 打開個 URL
- 應該睇到奶油色底 + 磚紅色 badge「NO-NONSENSE GOSPEL」
- 試 scroll 到底,填少少嘢,click 「生成 Prompt」
- 應該彈出輸出區,內容係繁中 prompt

**搞掂!**

---

## §4 Route B — 加入現有 Repo

**適合你有 `ivantheservant.github.io` 呢類個人 Pages repo。**

### 步驟

1. 入你現有 repo(例:`ivantheservant.github.io`)
2. Click `Add file` → `Create new file`
3. 上面檔名欄位輸入:`fellowship-planner/index.html`
    (打 `/` 會自動整返個 folder 出嚟)
4. 開另一個 tab,用 browser 打開本機嘅 `fellowship-planner.html`
5. 右 click → `View page source`,全選 copy(或者用編輯器打開 copy 全部內容)
6. 貼返入 GitHub 個新檔案
7. 底部 `Commit new file`
8. 等 1-3 分鐘
9. 打開:`https://ivantheservant.github.io/fellowship-planner/`

---

## §5 Route C — Ministry Tools Hub(建議長遠做法)

**最乾淨。將來所有工具(兒主、團契、查經、退修會...)都放埋一齊。**

### 建議結構

```
ivantheservant.github.io/ministry-tools/
├── index.html                      ← landing page(列出所有 tools)
├── kids-material/
│   ├── index.html
│   └── spec.md
├── fellowship-planner/
│   └── index.html                  ← 呢個 tool
├── bible-study/                    ← 將來
│   └── index.html
└── retreat-planner/                ← 將來
    └── index.html
```

### 步驟

1. 喺 `ivantheservant.github.io` repo 建立 folder `ministry-tools/`
2. 入面再建 `fellowship-planner/`,放 `index.html`
3. 同時可以預先建 `kids-material/` 放兒主 generator
4. 最上層 `ministry-tools/index.html` 做 landing page(可以遲啲先做)
5. Commit
6. 訪問:`https://ivantheservant.github.io/ministry-tools/fellowship-planner/`

### Landing Page 建議(future work)

做一頁簡單嘅 hub page,列出全部 tools,每個有:
- 工具名(中英)
- 一句話描述
- 「開始使用」連結
- 小 icon 或縮圖

風格跟個 tool 本身嘅 editorial paper aesthetic,令整個 ecosystem 感覺連貫。

---

## §6 部署後測試清單

Deploy 完之後,行完呢幾步先放心:

### 基本功能
- [ ] 網頁打開冇錯(睇到 header「團契週會設計器」)
- [ ] 字體 load 到(Cormorant Garamond + Noto Serif TC,唔係 fallback font)
- [ ] 紙質感 noise filter 有出(淡淡粒子感)

### 表單互動
- [ ] 所有下拉 select 可以點
- [ ] Checkbox 可以勾/反勾
- [ ] textarea / input 可以打字
- [ ] focus 狀態有紅色邊框

### 核心 workflow
- [ ] 完全唔填,直接 click「生成 Prompt」→ 應該都出到(空欄位會 skip)
- [ ] 填少少欄位,click「生成 Prompt」→ 輸出應該只包含有填嘅
- [ ] 填全部欄位,click「生成 Prompt」→ 輸出應該長啲
- [ ] 「Copy to Clipboard」→ 貼去 notepad,應該見到完整 prompt
- [ ] 「重設 Reset」→ 彈 confirm,click 是之後全部清空

### 手機測試
- [ ] 手機打開唔會亂
- [ ] Row grid 自動變單欄
- [ ] Checkbox group 變單欄
- [ ] Button 唔會 overflow

### 跨瀏覽器
- [ ] Chrome / Edge ✓
- [ ] Firefox ✓
- [ ] Safari(iPhone / Mac)✓
- [ ] 粵語輸入法打中文冇問題

---

## §7 部署後 Test Case(試一次完整 workflow)

**用以下情境 test 一次:**

### 情境:青年團契復活節聚會

填返以下欄位:

| 欄位 | 填咩 |
|---|---|
| 團契名稱 | 青年團契 |
| 聚會場合 | 復活節特別聚會 |
| 對象年齡層 | 青年 (18-25) |
| 屬靈光譜 | 混合 |
| 人數 | 8-15 人 |
| 主要語言 | 粵語 |
| 文化背景 | 香港為主 |
| 聚會總時長 | 90 |
| 場地類型 | 教會室內 |
| 預算範圍 | 少於 NZD $100 |
| 主要類型 | 綜合 |
| 節期 | 復活節 |
| 主題說明 | 復活嘅盼望 |
| 經文 | 哥林多前書 15:20-22 |
| 特殊考量(勾) | 有慕道友或初次參加者 |
| 破冰 | 需要 · 與主題相關 |
| 分享問題 | 中等屬靈 |
| 討論形式 | 開放討論 |
| 詩歌敬拜 | 混合 |
| 代禱形式 | 小組代禱 |

click「生成 Prompt」,應該睇到一段約 3000-4000 字嘅完整 prompt。

Copy 去 Claude/ChatGPT,應該會**先問你澄清問題**(例如:慕道友會唔會唔舒服就咁分享?點樣接待?),然後先設計活動。

**如果 AI 無問問題就直接設計** → 你個 prompt template 嘅「第一步:資料檢查」未生效,需要檢查 HTML。

---

## §8 常見問題 Troubleshooting

### Q1: 部署後打開係白頁

**可能原因:**
- Pages 未 build 完(等多陣,通常 1-3 分鐘,有時 5 分鐘)
- 檔案冇改名做 `index.html`
- 放咗去錯嘅 folder

**檢查:** 入 Settings → Pages,應該有綠色 tick + 網址

### Q2: 字體唔對,變咗系統預設字

**可能原因:** Google Fonts 被 block(某啲地區或網絡)

**解決方法:** 喺 HTML 入面將 Google Fonts 嘅 `<link>` 改做其他 CDN,或者 self-host 啲字體。唔緊急,fallback font 都能睇。

### Q3: Click「Copy」冇反應

**可能原因:** 舊瀏覽器唔支援 `navigator.clipboard` API

**已處理:** HTML 入面已經有 `execCommand` fallback,照用冇問題

### Q4: 手機 rendering 錯亂

**檢查:**
- `<meta name="viewport">` 有冇 load 到
- 試另一個瀏覽器
- Clear cache

### Q5: 想改欄位 / 選項 / 措辭

**直接改 HTML:**
- 欄位名:搵 `<label class="label">...`
- 下拉選項:搵 `<option>...`
- Prompt 內容:搵 JS function `buildPrompt()`,改入面嘅 template string

改完 commit,1-3 分鐘後生效。

### Q6: 想加新欄位

步驟:
1. HTML 入面加 `<input>` / `<select>` / `<textarea>`,記得有 `id`
2. JS `buildPrompt()` 開頭加 `const xxx = getVal('id');`
3. JS 底部適當 section 加返 `line('欄位名', d.xxx)`
4. Commit

---

## §9 更新 / 迭代流程

試用過幾次之後,會發現有啲地方想改。建議流程:

### 小修小補(改字眼、改選項、調色)
- 直接喺 GitHub 網頁 edit `index.html`
- Commit → 自動 deploy
- 適合:typo、多加/少減一個選項、改色

### 中型改動(加 section、改表單結構)
- 本機用 editor(VS Code)開 HTML
- 改完 preview 過
- 用 Git push 上去(或者 drag and drop re-upload)
- 適合:加新 § 區塊、改 prompt template、改排版

### 大改(加功能 feature)
- 想加 localStorage(記住上次填過嘅)
- 想加多語言切換
- 想加 preset(例:「ECF 青年團常用」一 click 填好)
- **建議**:開 Claude Code session 一齊做,由我幫你寫

---

## §10 與兒主 Generator 整合建議

如果你將兩個工具(兒主 + 團契)都擺上 Pages:

### 視覺統一
- 兩個都用緊相同色盤 + 字體 + § 裝飾
- 加埋 landing page 就會好似一個 ministry toolkit brand
- 可以共用 favicon / 小 logo

### 導航連貫
喺每個 tool 嘅 footer 加返:
```html
<footer>
  探索更多工具 · More tools:
  <a href="../kids-material/">兒主教材產生器</a> ·
  <a href="../fellowship-planner/">團契週會設計器</a>
</footer>
```

### 品牌訊息
可以喺 landing page 加段你嘅使命描述:

> 「呢啲工具係 No-Nonsense Gospel 嘅一部分 ——
> 為華人教會同工而設,免費、開源、尊重你嘅選擇。
> 我哋唔揸住你嘅資料,唔收你錢,亦唔取代你嘅判斷。
> 只係想用 AI,幫你做緊嘅牧養工作,減少重複勞動,
> 讓你有更多時間關顧弟兄姊妹。」

---

## §11 推廣建議

Deploy 好之後,可以點樣俾其他牧者/同工用?

### 第一波:你 trusted 嘅人
- ECF 聖道堂同工(e.g. 團契導師、執事)
- Agape Interlink 相關教會
- Patreon 支持者(可以寫一篇介紹 post)

### 第二波:公開發佈
- YouTube 短片 demo(你自己嘅 channel)
- Facebook 群組(基督徒同工網絡)
- 寫一篇 blog / Patreon 長文,附上用法 + 試用案例

### 收 feedback
- 加個 Google Form 連結喺 footer,收改善建議
- 或者叫用戶直接 email / Telegram 你
- 每個月 review 一次 feedback,做一個 v1.1 / v1.2

---

## §12 Maintenance Checklist

### 每月一次
- [ ] 試用 tool 一次,確認仲 work
- [ ] Check GitHub Pages 有冇 fail

### 每季一次
- [ ] 睇 feedback,決定下次 iteration 要改咩
- [ ] 更新 footer 日期

### 每年一次
- [ ] 大翻新一次(睇有冇新 features 想加)
- [ ] 更新 screenshots(如有 documentation)

---

## §13 File Inventory

呢個 project 成熟之後應該有嘅檔案:

```
fellowship-planner/
├── index.html              ← 主程式(52KB)
├── DEPLOYMENT_GUIDE.md     ← 呢份文件
├── README.md               ← GitHub 主頁描述(可選)
└── CHANGELOG.md            ← 版本記錄(可選)
```

**記得**:所有檔案都 save 一份去 `C:\ivan\ClaudeMemory\outputs\FellowshipPlanner\` 做備份。

---

## §14 版本記錄

| 版本 | 日期 | 改動 |
|---|---|---|
| v1.0 | 2026-04-24 | 初次發佈。55 個欄位,編輯式 paper aesthetic,繁中+英雙語 label |

---

## §15 支援

有問題/建議:
- Email: (你嘅 contact)
- YouTube: [@nononsensegospel](https://www.youtube.com/@nononsensegospel)
- 或者開新 Claude chat 叫 Ivan 跟進

---

*「服事,唔一定要複雜。複雜嘅係人,簡單嘅係工具。
工具應該減少你嘅負擔,唔係加你嘅負擔。」*

— 串嘴大叔 Ivan
