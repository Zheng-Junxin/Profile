# Public Profile Homepage Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rebuild the existing `Profile` repository as a polished static public personal profile homepage and add the requested embedded software engineer work experience.

**Architecture:** Keep the project as a single GitHub Pages compatible static page. `index.html` owns the HTML, CSS, and minimal JavaScript needed for smooth anchor navigation; existing assets `avatar.jpg` and `transcript.pdf` remain unchanged.

**Tech Stack:** Plain HTML5, CSS3, minimal browser JavaScript, local image/PDF assets, optional Python/Node one-off verification scripts.

---

## File Structure

- Modify: `index.html`
  - Replace the current resume-sheet style with a UTF-8 public homepage and verify no mojibake remains.
  - Include responsive CSS, semantic sections, accessible link text, and the requested work experience.
- Modify: `README.md`
  - Replace mojibake instructions with clear project usage notes.
- Keep unchanged: `avatar.jpg`
  - Used in the hero section.
- Keep unchanged: `transcript.pdf`
  - Linked from hero and education sections.
- Use existing: `.gitignore`
  - Keeps `.superpowers/` preview artifacts out of Git.

---

### Task 1: Add Static Content Verification

**Files:**
- Modify: `index.html`
- Modify: `README.md`

- [ ] **Step 1: Run a failing required-content check before implementation**

Run:

```powershell
node -e "const fs=require('fs'); const html=fs.readFileSync('index.html','utf8'); const readme=fs.readFileSync('README.md','utf8'); const required=['郑俊鑫','嵌入式软件工程师','深圳市盛能杰科技有限公司','2026.07.01-至今','avatar.jpg','transcript.pdf']; const mojibake=['閮','涓','鍩','锟','é','ä','å','ç','æ',String.fromCharCode(0xfffd)]; const missing=required.filter(x=>!html.includes(x)); const bad=mojibake.filter(x=>html.includes(x)||readme.includes(x)); if(missing.length||bad.length){ console.error(JSON.stringify({missing,bad},null,2)); process.exit(1); } console.log('content-ok');"
```

Expected before implementation: FAIL because `嵌入式软件工程师`, `深圳市盛能杰科技有限公司`, and `2026.07.01-至今` are missing.

- [ ] **Step 2: Replace `index.html` with the homepage implementation**

Implementation requirements:

```text
Use a full HTML document with:
- <html lang="zh-CN">
- <meta charset="UTF-8">
- Header nav anchors: #about, #experience, #skills, #projects, #honors, #contact
- Hero with 郑俊鑫, 嵌入式软件工程师, avatar.jpg, mailto link, transcript.pdf link
- Highlights for 汕头大学, 电子与计算机工程, GPA 3.63/5.0, CET-6, 广东汕头
- Experience section containing exactly:
  2026.07.01-至今 深圳市盛能杰科技有限公司 嵌入式软件工程师
- Education, skills, projects, honors, self-evaluation, and contact sections
- Responsive CSS using media queries for <= 760px
- No external build step and no dependency on remote CSS/JS
```

- [ ] **Step 3: Replace `README.md` with clean UTF-8 usage notes**

Use this content:

```markdown
# Profile

个人简介静态网页，适合部署到 GitHub Pages。

## 文件说明

- `index.html`: 个人主页入口。
- `avatar.jpg`: 首页头像图片。
- `transcript.pdf`: 成绩单 PDF，页面中的“查看成绩单”链接会打开该文件。

## 本地预览

直接用浏览器打开 `index.html`，或在项目根目录启动任意静态文件服务器。
```

- [ ] **Step 4: Run the required-content check again**

Run:

```powershell
node -e "const fs=require('fs'); const html=fs.readFileSync('index.html','utf8'); const readme=fs.readFileSync('README.md','utf8'); const required=['郑俊鑫','嵌入式软件工程师','深圳市盛能杰科技有限公司','2026.07.01-至今','avatar.jpg','transcript.pdf']; const mojibake=['閮','涓','鍩','锟','é','ä','å','ç','æ',String.fromCharCode(0xfffd)]; const missing=required.filter(x=>!html.includes(x)); const bad=mojibake.filter(x=>html.includes(x)||readme.includes(x)); if(missing.length||bad.length){ console.error(JSON.stringify({missing,bad},null,2)); process.exit(1); } console.log('content-ok');"
```

Expected after implementation: PASS with `content-ok`.

---

### Task 2: Validate Static Page Behavior

**Files:**
- Verify: `index.html`
- Verify: `avatar.jpg`
- Verify: `transcript.pdf`

- [ ] **Step 1: Verify asset references exist**

Run:

```powershell
node -e "const fs=require('fs'); const html=fs.readFileSync('index.html','utf8'); const refs=['avatar.jpg','transcript.pdf']; const missing=refs.filter(ref=>!fs.existsSync(ref)||!html.includes(ref)); if(missing.length){ console.error(JSON.stringify({missing},null,2)); process.exit(1); } console.log('assets-ok');"
```

Expected: PASS with `assets-ok`.

- [ ] **Step 2: Verify links and anchors are present**

Run:

```powershell
node -e "const fs=require('fs'); const html=fs.readFileSync('index.html','utf8'); const q=String.fromCharCode(34); const required=['href='+q+'#about'+q,'href='+q+'#experience'+q,'href='+q+'#skills'+q,'href='+q+'#projects'+q,'href='+q+'#honors'+q,'href='+q+'#contact'+q,'href='+q+'mailto:2323857919@qq.com'+q,'href='+q+'transcript.pdf'+q]; const missing=required.filter(x=>!html.includes(x)); if(missing.length){ console.error(JSON.stringify({missing},null,2)); process.exit(1); } console.log('links-ok');"
```

Expected: PASS with `links-ok`.

- [ ] **Step 3: Start a local static server and verify HTTP 200**

Run:

```powershell
Start-Process -FilePath python -ArgumentList "-m", "http.server", "8099", "--bind", "127.0.0.1" -WorkingDirectory "." -WindowStyle Hidden
Start-Sleep -Seconds 1
Invoke-WebRequest -Uri http://127.0.0.1:8099/index.html -UseBasicParsing -TimeoutSec 5 | Select-Object StatusCode
```

Expected: `StatusCode` is `200`.

- [ ] **Step 4: Commit implementation**

Run:

```powershell
git add index.html README.md docs/superpowers/plans/2026-07-03-public-profile-homepage.md
git commit -m "feat: build public profile homepage"
```

Expected: Commit succeeds and includes the homepage, README, and implementation plan.
