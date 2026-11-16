# AGENTS.md - 專案開發與擴充規範

## 1. 專案目的
本專案為「個人技術與學習筆記網站」，旨在以清晰、易讀的網頁形式整理課堂講義與自學筆記。
本文件的目的是讓 AI 協作時，能完全理解網站架構與設計風格，並能快速、無誤差地新增或修改筆記頁面。

## 2. 資料夾與檔案命名規則
- `index.html`：網站首頁，負責顯示網站標題、簡介，以及所有筆記的導覽卡片列表。
- `css/style.css`：全站共用的 CSS 樣式表。**嚴禁**在個別 HTML 檔案中寫行內樣式（Inline CSS）或自建 `<style>` 標籤。
- `lessons/`：所有筆記內頁皆必須存放在此資料夾中。
  - **命名格式**：`[兩位數編號]-[英文小寫關鍵字].html`（例如：`01-git-basics.html`、`02-prompt-engineering.html`）。

## 3. 視覺與排版風格規範
- **色彩系統**：採用簡約護眼風格。背景色 `#F8FAFC`，卡片與文章底色 `#FFFFFF`，主色調（導覽列、重點標題）為深藍 `#1E3A8A`，強調色（標籤、按鈕）為天藍 `#0284C7`。
- **字體與閱讀體驗**：內文字級 `16px`，行高 `1.7`，最大內容寬度限制為 `800px` 並置中，確保長文閱讀舒適。
- **響應式設計**：所有頁面必須支援手機與桌面瀏覽（使用 Flexbox / Grid 排版）。

## 4. 頁面 HTML 結構標準
### A. 首頁 (`index.html`)
- `<header>`：包含網站主標題與一句話簡介。
- `<main class="card-grid">`：每篇筆記對應一個 `<article class="lesson-card">`，內含：
  1. 分類標籤 (`<span class="tag">`)
  2. 文章標題 (`<h2>`)
  3. 兩句話以內的摘要 (`<p>`)
  4. 連結按鈕 (`<a href="lessons/檔名.html" class="btn">閱讀筆記 →</a>`)

### B. 筆記內頁 (`lessons/*.html`)
- 必須引入共用樣式：`<link rel="stylesheet" href="../css/style.css">`
- `<nav class="breadcrumb">`：頂部必須包含返回首頁的連結（`<a href="../index.html">← 返回筆記列表</a>`）。
- `<article class="lesson-content">`：
  1. `<header>`：包含文章標題 `<h1>`、發布日期與分類標籤。
  2. `<section>`：每個大段落使用 `<h2>` 作為小標題，重點提示使用 `<blockquote>` 包裝，程式碼使用 `<pre><code>` 包裝。

## 5. AI 新增頁面時的標準作業程序 (SOP)
當使用者要求「新增一篇關於 XXX 的筆記/頁面」時，AI 必須嚴格執行以下三個步驟：
1. **建立內頁**：在 `lessons/` 資料夾下，依照編號順序建立新的 HTML 檔案，並完全套用「4-B 筆記內頁」的 HTML 結構與 `../css/style.css`。
2. **更新首頁**：打開 `index.html`，在 `<main class="card-grid">` 的最下方（或依編號順序），新增對應的 `<article class="lesson-card">` 卡片連結。
3. **自我檢查**：確認所有相對路徑（`../index.html`、`../css/style.css`、`lessons/...`）皆正確無誤，且未修改既有 CSS 變數。


