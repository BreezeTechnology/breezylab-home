# 網站內容與業務計劃書對齊 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Edit the deployed `dist/index.html` so its copy (services, portfolio/案例, about timeline) is structurally consistent with `業務計劃書.md`, without disclosing financial figures or unsigned deals.

**Architecture:** Single static HTML file, content-only edits via string replacement. No build step involved — `dist/index.html` is hand-edited directly, matching this repo's existing convention (confirmed via `git log`: `src/pug/index.pug` has never been customized, only Bootstrap-version bumps; all real content commits touch `dist/index.html` directly).

**Tech Stack:** Plain HTML + Bootstrap 5 classes already used on the page. No new dependencies, no JS changes.

## Global Constraints

- Only `dist/index.html` may be modified. Do not touch `src/pug/*`, `privacy-policy.html`, `terms.html`, or any CSS/JS file.
- No financial figures (revenue, loss, growth %, USD/month) anywhere in the new copy.
- No mention of the in-talks, unsigned Hong Kong Web3 partnership.
- All new/changed copy is in Traditional Chinese, matching the existing page's register (see commit `a24b3a9 改成繁体`).
- Do not run `git commit` — the user will commit changes themselves.
- After every task, reload `dist/index.html` in a browser (`open dist/index.html`) or otherwise confirm the file is well-formed (no truncated tags) before moving to the next task.

---

### Task 1: Rewrite the two mismatched service tiles

**Files:**
- Modify: `dist/index.html:62-77` (the second and third `.col-md-4` tiles inside `<section class="page-section" id="services">`)

**Interfaces:** None — this is a self-contained content swap, no other task depends on exact wording here.

- [ ] **Step 1: Replace the "應用設計與開發" tile**

Find this block (currently lines 62-68):

```html
                    <div class="col-md-4">
                        <span class="fa-stack fa-4x">
                            <i class="fas fa-circle fa-stack-2x text-primary"></i>
                            <i class="fas fa-mobile-screen-button fa-stack-1x fa-inverse"></i>
                        </span>
                        <h4 class="my-3">應用設計與開發</h4>
                        <p class="text-muted">憑藉多年的開發經驗和創新思維，我們為客戶設計和開發滿足用戶需求的手機應用程式，特別是應用AI技術的智能應用程式。</p>
                    </div>
```

Replace with:

```html
                    <div class="col-md-4">
                        <span class="fa-stack fa-4x">
                            <i class="fas fa-circle fa-stack-2x text-primary"></i>
                            <i class="fas fa-mobile-screen-button fa-stack-1x fa-inverse"></i>
                        </span>
                        <h4 class="my-3">自有AI音樂音訊應用</h4>
                        <p class="text-muted">我們自主研發並持續營運多款AI音樂與音訊類手機應用程式，涵蓋人聲分離、鈴聲製作、語音記錄及音訊編輯等功能，服務全球用戶。</p>
                    </div>
```

- [ ] **Step 2: Replace the "出海營運與推廣" tile**

Find this block (currently lines 70-77):

```html
                    <div class="col-md-4">
                        <span class="fa-stack fa-4x">
                            <i class="fas fa-circle fa-stack-2x text-primary"></i>
                            <i class="fas fa-earth-americas fa-stack-1x fa-inverse"></i>
                        </span>
                        <h4 class="my-3">出海營運與推廣</h4>
                        <p class="text-muted">針對希望將產品推廣到海外市場的客戶，我們提供全方位的出海代營運服務。我們擁有豐富的全球化推廣策略，能夠協助客戶分析目標市場，制定本地化營運方案，並持續進行數據分析與策略優化，協助客戶實現海外市場的快速拓展和穩定增長。</p>
                    </div>
```

Replace with:

```html
                    <div class="col-md-4">
                        <span class="fa-stack fa-4x">
                            <i class="fas fa-circle fa-stack-2x text-primary"></i>
                            <i class="fas fa-earth-americas fa-stack-1x fa-inverse"></i>
                        </span>
                        <h4 class="my-3">全球用戶營運與成長</h4>
                        <p class="text-muted">我們透過持續的產品迭代、用戶增長及本地化推廣，將自有應用程式推廣至全球市場，建立穩定且持續增長的訂閱用戶群。</p>
                    </div>
```

- [ ] **Step 3: Verify the file is still well-formed**

Run: `python3 -c "import re; s=open('dist/index.html').read(); print('services tiles:', s.count('col-md-4'))"`
Expected: `services tiles: 3` (the three service pillars, unchanged count — confirms no tag was accidentally deleted).

Also run: `grep -c "自有AI音樂音訊應用\|全球用戶營運與成長" dist/index.html`
Expected: `2`

No commit — proceed to Task 2.

---

### Task 2: Rewrite the portfolio grid to 2 cards (app product line first, then consulting)

**Files:**
- Modify: `dist/index.html:88-134` (the `.row` inside `<section ... id="portfolio">`)

**Interfaces:**
- Produces: two portfolio-link anchors pointing at `#portfolioModal1` and `#portfolioModal2` — Task 3 replaces the modal markup those anchors point to. The `id` values (`portfolioModal1`, `portfolioModal2`) must match exactly what Task 3 defines.

- [ ] **Step 1: Replace the entire 3-card `.row` with a 2-card row**

Find the whole block from `<div class="row">` (line 88) through its closing `</div>` (line 134) — i.e. everything between (and including) these two lines:

```html
                <div class="row">
```
... (3 `.col-lg-4.col-sm-6.mb-4` cards) ...
```html
                </div>
```

Replace the full contents with:

```html
                <div class="row justify-content-center">
                    <div class="col-lg-6 col-md-6 mb-4">
                        <!-- Portfolio item 1-->
                        <div class="portfolio-item">
                            <a class="portfolio-link" data-bs-toggle="modal" href="#portfolioModal1">
                                <div class="portfolio-hover">
                                    <div class="portfolio-hover-content"><i class="fas fa-plus fa-3x"></i></div>
                                </div>
                                <img class="img-fluid" src="assets/img/portfolio/1.jpg" alt="..." />
                            </a>
                            <div class="portfolio-caption">
                                <div class="portfolio-caption-heading">AI音樂音訊App產品線</div>
                                <div class="portfolio-caption-subheading text-muted">自有產品，服務全球用戶</div>
                            </div>
                        </div>
                    </div>
                    <div class="col-lg-6 col-md-6 mb-4">
                        <!-- Portfolio item 2-->
                        <div class="portfolio-item">
                            <a class="portfolio-link" data-bs-toggle="modal" href="#portfolioModal2">
                                <div class="portfolio-hover">
                                    <div class="portfolio-hover-content"><i class="fas fa-plus fa-3x"></i></div>
                                </div>
                                <img class="img-fluid" src="assets/img/portfolio/2.jpg" alt="..." />
                            </a>
                            <div class="portfolio-caption">
                                <div class="portfolio-caption-heading">新加坡企業技術諮詢項目</div>
                                <div class="portfolio-caption-subheading text-muted">技術諮詢與培訓</div>
                            </div>
                        </div>
                    </div>
                </div>
```

Note: this also re-enables the modal links. The three cards previously had `href="#"` with the real modal href commented out (e.g. `href="#"><!--href="#portfolioModal1">-->`) — meaning no card was actually clickable before. The replacement above uses live `href="#portfolioModalN"` since Task 3 will give those modals real, finished content (the old lorem-ipsum modals were presumably left disabled on purpose).

- [ ] **Step 2: Verify**

Run: `grep -c 'col-lg-6 col-md-6 mb-4' dist/index.html`
Expected: `2`

Run: `grep -c 'portfolio-caption-heading' dist/index.html`
Expected: `2`

No commit — proceed to Task 3.

---

### Task 3: Replace portfolio modal content (modal 1 + modal 2), delete unused modals 3–6

**Files:**
- Modify: `dist/index.html` — the six `<div class="portfolio-modal modal fade" id="portfolioModalN" ...>` blocks near the end of `<body>`, currently modals 1 through 6.

**Interfaces:**
- Consumes: `id="portfolioModal1"` and `id="portfolioModal2"` anchors from Task 2 — these ids must match exactly.

- [ ] **Step 1: Replace modal 1 (currently the 金融客戶敏捷培訓 lorem-ipsum-free one) with the App product line**

Find:

```html
        <!-- Portfolio item 1 modal popup-->
        <div class="portfolio-modal modal fade" id="portfolioModal1" tabindex="-1" role="dialog" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="close-modal" data-bs-dismiss="modal"><img src="assets/img/close-icon.svg" alt="Close modal" /></div>
                    <div class="container">
                        <div class="row justify-content-center">
                            <div class="col-lg-8">
                                <div class="modal-body">
                                    <!-- Project details-->
                                    <h2 class="text-uppercase">金融客戶敏捷培訓</h2>
                                    <p class="item-intro text-muted">為企業交付多期敏捷培訓。</p>
                                    <img class="img-fluid d-block mx-auto" src="assets/img/portfolio/1.jpg" alt="..." />
                                    <p>Use this area to describe your project. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Est blanditiis dolorem culpa incidunt minus dignissimos deserunt repellat aperiam quasi sunt officia expedita beatae cupiditate, maiores repudiandae, nostrum, reiciendis facere nemo!</p>
                                    <ul class="list-inline">
                                        <li>
                                            <strong>Client:</strong>
                                            金融客戶
                                        </li>
                                        <li>
                                            <strong>Category:</strong>
                                            技術培訓
                                        </li>
                                    </ul>
                                    <button class="btn btn-primary btn-xl text-uppercase" data-bs-dismiss="modal" type="button">
                                        <i class="fas fa-xmark me-1"></i>
                                        Close Project
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
```

Replace with:

```html
        <!-- Portfolio item 1 modal popup-->
        <div class="portfolio-modal modal fade" id="portfolioModal1" tabindex="-1" role="dialog" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="close-modal" data-bs-dismiss="modal"><img src="assets/img/close-icon.svg" alt="Close modal" /></div>
                    <div class="container">
                        <div class="row justify-content-center">
                            <div class="col-lg-8">
                                <div class="modal-body">
                                    <!-- Project details-->
                                    <h2 class="text-uppercase">AI音樂音訊App產品線</h2>
                                    <p class="item-intro text-muted">自主研發並持續營運，已在Apple App Store正式上架</p>
                                    <img class="img-fluid d-block mx-auto" src="assets/img/portfolio/1.jpg" alt="..." />
                                    <p>我們目前已在Apple App Store上線四款AI音樂及音訊類應用程式，面向全球用戶：</p>
                                    <ul class="list-unstyled">
                                        <li class="mb-2"><strong>Stemify：</strong>AI人聲分離，支持提取人聲、伴奏或各類樂器音軌，並可自由混音。<br /><a href="https://apps.apple.com/us/app/ai-vocal-remover-stemify/id6698862908" target="_blank" rel="noopener">前往App Store</a></li>
                                        <li class="mb-2"><strong>Ringtone Maker &amp; AI Cover：</strong>鈴聲製作及AI變聲，支持個性化鈴聲創作及AI音色翻唱。<br /><a href="https://apps.apple.com/us/app/ringtone-maker-ai-cover/id6475240863" target="_blank" rel="noopener">前往App Store</a></li>
                                        <li class="mb-2"><strong>語音備忘錄：</strong>AI智能錄音，支持自動轉錄及智能整理。<br /><a href="https://apps.apple.com/us/app/ai-voice-recorder-transcribe/id6468926150" target="_blank" rel="noopener">前往App Store</a></li>
                                        <li class="mb-2"><strong>Audio Editor - Audiolab：</strong>專業音頻編輯工具，支持多軌編輯、音效處理及格式轉換。<br /><a href="https://apps.apple.com/us/app/audio-editor-audiolab/id6446192816" target="_blank" rel="noopener">前往App Store</a></li>
                                    </ul>
                                    <button class="btn btn-primary btn-xl text-uppercase" data-bs-dismiss="modal" type="button">
                                        <i class="fas fa-xmark me-1"></i>
                                        Close Project
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
```

- [ ] **Step 2: Replace modal 2 with the Singapore consulting project**

Find:

```html
        <!-- Portfolio item 2 modal popup-->
        <div class="portfolio-modal modal fade" id="portfolioModal2" tabindex="-1" role="dialog" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="close-modal" data-bs-dismiss="modal"><img src="assets/img/close-icon.svg" alt="Close modal" /></div>
                    <div class="container">
                        <div class="row justify-content-center">
                            <div class="col-lg-8">
                                <div class="modal-body">
                                    <!-- Project details-->
                                    <h2 class="text-uppercase">Project Name</h2>
                                    <p class="item-intro text-muted">Lorem ipsum dolor sit amet consectetur.</p>
                                    <img class="img-fluid d-block mx-auto" src="assets/img/portfolio/2.jpg" alt="..." />
                                    <p>Use this area to describe your project. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Est blanditiis dolorem culpa incidunt minus dignissimos deserunt repellat aperiam quasi sunt officia expedita beatae cupiditate, maiores repudiandae, nostrum, reiciendis facere nemo!</p>
                                    <ul class="list-inline">
                                        <li>
                                            <strong>Client:</strong>
                                            Explore
                                        </li>
                                        <li>
                                            <strong>Category:</strong>
                                            Graphic Design
                                        </li>
                                    </ul>
                                    <button class="btn btn-primary btn-xl text-uppercase" data-bs-dismiss="modal" type="button">
                                        <i class="fas fa-xmark me-1"></i>
                                        Close Project
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
```

Replace with:

```html
        <!-- Portfolio item 2 modal popup-->
        <div class="portfolio-modal modal fade" id="portfolioModal2" tabindex="-1" role="dialog" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="close-modal" data-bs-dismiss="modal"><img src="assets/img/close-icon.svg" alt="Close modal" /></div>
                    <div class="container">
                        <div class="row justify-content-center">
                            <div class="col-lg-8">
                                <div class="modal-body">
                                    <!-- Project details-->
                                    <h2 class="text-uppercase">新加坡企業技術諮詢項目</h2>
                                    <p class="item-intro text-muted">技術諮詢與培訓</p>
                                    <img class="img-fluid d-block mx-auto" src="assets/img/portfolio/2.jpg" alt="..." />
                                    <p>我們透過香港公司為新加坡企業客戶承接並完成技術諮詢項目，協助客戶提升研發效率與團隊協作實踐，體現了香港公司作為國際業務簽約平台的角色。</p>
                                    <ul class="list-inline">
                                        <li>
                                            <strong>Client:</strong>
                                            新加坡企業
                                        </li>
                                        <li>
                                            <strong>Category:</strong>
                                            技術諮詢
                                        </li>
                                    </ul>
                                    <button class="btn btn-primary btn-xl text-uppercase" data-bs-dismiss="modal" type="button">
                                        <i class="fas fa-xmark me-1"></i>
                                        Close Project
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
```

- [ ] **Step 3: Delete modals 3, 4, 5, and 6 entirely**

These four blocks are never referenced by any `href` on the page (confirmed: the old cards used `href="#"` with the modal href commented out, and Task 2 only created `#portfolioModal1` and `#portfolioModal2` anchors). Delete each full block, from its `<!-- Portfolio item N modal popup-->` comment down to its closing `</div>` before the next comment (or before `<!-- Bootstrap core JS-->` for modal 6). For example, delete this whole block for modal 3:

```html
        <!-- Portfolio item 3 modal popup-->
        <div class="portfolio-modal modal fade" id="portfolioModal3" tabindex="-1" role="dialog" aria-hidden="true">
            ...
        </div>
```

Repeat identically for modal 4, modal 5, and modal 6 (same structure, only the `id`, image path, and placeholder text differ — delete the whole `<div class="portfolio-modal ...">...</div>` for each).

- [ ] **Step 4: Verify**

Run: `grep -o 'id="portfolioModal[0-9]"' dist/index.html`
Expected: exactly two lines, `id="portfolioModal1"` and `id="portfolioModal2"` (each appearing once — the anchor in the grid and the modal itself both use the same string, so `grep -c` would show 2 total per id if you count both the `href="#portfolioModalN"` and `id="portfolioModalN"` separately; this command only matches the `id="..."` form, so it isolates the modals).

Run: `grep -c 'Project Name\|Lorem ipsum dolor sit amet consectetur\|Use this area to describe your project' dist/index.html`
Expected: `0` (no leftover template placeholder text anywhere on the page).

No commit — proceed to Task 4.

---

### Task 4: Extend the About-us timeline with two vague, number-free 2024 entries

**Files:**
- Modify: `dist/index.html:165-186` (the `<ul class="timeline">` inside `<section ... id="about">`)

**Interfaces:** None — self-contained insertion between two existing `<li>` elements.

- [ ] **Step 1: Insert two new `<li>` entries between the "2024年7月 在香港註冊公司" entry and the closing "期待與您合作" entry**

Find:

```html
                    <li class="timeline-inverted">
                        <div class="timeline-image"><img class="rounded-circle img-fluid" src="assets/img/about/4.png" alt="..." /></div>
                        <div class="timeline-panel">
                            <div class="timeline-heading">
                                <h4>2024年7月</h4>
                                <h4 class="subheading">在香港註冊公司</h4>
                            </div>
                            <div class="timeline-body"><p class="text-muted">為了方便開展業務並服務全球化客戶，我們在香港正式註冊了椰風科技有限公司（Breeze Technology Co., Limited）。公司致力於整合在技術諮詢、應用開發和海外營運等方面的優勢資源，謀求為各類客戶提供更加專業和全面的解決方案。</p></div>
                        </div>
                    </li>
                    <li class="timeline-inverted">
                        <div class="timeline-image">
                            <h4>
                                期待
                                <br />
                                與您
                                <br />
                                合作
                            </h4>
                        </div>
                    </li>
```

Replace with:

```html
                    <li class="timeline-inverted">
                        <div class="timeline-image"><img class="rounded-circle img-fluid" src="assets/img/about/4.png" alt="..." /></div>
                        <div class="timeline-panel">
                            <div class="timeline-heading">
                                <h4>2024年7月</h4>
                                <h4 class="subheading">在香港註冊公司</h4>
                            </div>
                            <div class="timeline-body"><p class="text-muted">為了方便開展業務並服務全球化客戶，我們在香港正式註冊了椰風科技有限公司（Breeze Technology Co., Limited）。公司致力於整合在技術諮詢、應用開發和海外營運等方面的優勢資源，謀求為各類客戶提供更加專業和全面的解決方案。</p></div>
                        </div>
                    </li>
                    <li>
                        <div class="timeline-image"><img class="rounded-circle img-fluid" src="assets/img/about/1.jpg" alt="..." /></div>
                        <div class="timeline-panel">
                            <div class="timeline-heading">
                                <h4>2024年下半年</h4>
                                <h4 class="subheading">App產品線陸續上線</h4>
                            </div>
                            <div class="timeline-body"><p class="text-muted">我們自主研發的AI音樂與音訊類手機應用程式陸續在Apple App Store上線，並持續投入產品優化與用戶增長，逐步建立起穩定的全球用戶群體。</p></div>
                        </div>
                    </li>
                    <li class="timeline-inverted">
                        <div class="timeline-image"><img class="rounded-circle img-fluid" src="assets/img/about/4.jpg" alt="..." /></div>
                        <div class="timeline-panel">
                            <div class="timeline-heading">
                                <h4>2024年底</h4>
                                <h4 class="subheading">開展技術諮詢業務</h4>
                            </div>
                            <div class="timeline-body"><p class="text-muted">我們開始為企業客戶提供技術諮詢與培訓服務，並持續拓展香港及東南亞地區的合作機會。</p></div>
                        </div>
                    </li>
                    <li class="timeline-inverted">
                        <div class="timeline-image">
                            <h4>
                                期待
                                <br />
                                與您
                                <br />
                                合作
                            </h4>
                        </div>
                    </li>
```

Note: `assets/img/about/1.jpg` and `assets/img/about/4.jpg` are both existing, currently-unused image files in `dist/assets/img/about/` (confirmed via `ls`) — distinct from `2.jpg`, `3.jpg`, and `4.png` which the existing timeline entries already use, so no entry duplicates an image.

- [ ] **Step 2: Verify**

Run: `grep -c '<li' dist/index.html`
Expected: previous count + 2 (if you don't know the previous count, instead run the next check, which is sufficient on its own).

Run: `grep -c '2024年下半年\|2024年底' dist/index.html`
Expected: `2`

Run: `grep -c 'assets/img/about/1.jpg\|assets/img/about/4.jpg' dist/index.html`
Expected: `2` (one each)

No commit — this is the final task. Do not run `git commit`; leave the working tree changes for the user to review and commit themselves.

---

## Final Verification (after Task 4)

- [ ] Run `open dist/index.html` (or equivalent) and manually check in a browser:
  - Services section shows the two reworded tiles without claiming client work for the apps.
  - Portfolio section shows exactly 2 cards (App product line, then Singapore consulting), both clickable, both modals show full real content with no lorem ipsum.
  - About timeline shows 5 entries total ending in "期待與您合作": 組建團隊(2023/04) → 開展多種類型的業務(2023/12) → 在香港註冊公司(2024/07) → App產品線陸續上線(2024下半年) → 開展技術諮詢業務(2024年底) → 期待與您合作.
  - No dollar amounts, percentages, or mention of the Hong Kong Web3 negotiation appear anywhere on the page.
- [ ] Run `grep -rn 'USD\|美元\|港元\|萬港元\|Web3企業' dist/index.html` — expect no output (confirms no financial figures or unsigned-deal references leaked in).
