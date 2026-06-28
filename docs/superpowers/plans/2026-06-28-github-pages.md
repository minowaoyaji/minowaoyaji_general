# GitHub Pages Publishing Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish the two lines in `test` as a static page at `https://minowaoyaji.github.io/minowaoyaji_general/`.

**Architecture:** Add one UTF-8 HTML entry point at the repository root and publish the root of `main` with GitHub Pages' branch deployment. Keep the original `test` file unchanged and avoid a build system or deployment workflow.

**Tech Stack:** HTML5, Git, GitHub Pages

---

## File Map

- Create `index.html`: browser entry point that displays the two lines from `test`.
- Keep `test`: original source text, unchanged.
- Use GitHub repository settings: configure Pages to deploy from `main` and `/ (root)`.

### Task 1: Add the Static Page

**Files:**
- Create: `index.html`
- Verify unchanged: `test`

- [ ] **Step 1: Run the pre-implementation check**

Run:

```bash
test ! -e index.html
```

Expected: exit status 0, confirming that the page does not exist yet.

- [ ] **Step 2: Create the minimal HTML document**

Create `index.html` with exactly:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>test</title>
</head>
<body>
  <div>test</div>
  <div>test2</div>
</body>
</html>
```

- [ ] **Step 3: Verify the page and source text**

Run:

```bash
python3 -c 'from pathlib import Path; p=Path("index.html").read_text(); assert "<meta charset=\"utf-8\">" in p; assert "<div>test</div>" in p; assert "<div>test2</div>" in p; assert Path("test").read_text() == "test\ntest2\n"'
```

Expected: exit status 0 with no output.

- [ ] **Step 4: Commit the static page**

Run:

```bash
git add index.html
git commit -m "feat: add GitHub Pages entry point"
```

Expected: one new commit containing only `index.html`.

### Task 2: Publish and Verify GitHub Pages

**Files:**
- No local file changes.
- Configure: GitHub Pages repository setting.

- [ ] **Step 1: Push the local commits**

Run:

```bash
git push origin main
```

Expected: the design, plan, and page commits are uploaded to `origin/main`.

- [ ] **Step 2: Configure the Pages source**

Open `https://github.com/minowaoyaji/minowaoyaji_general/settings/pages`. Under **Build and deployment**, select **Deploy from a branch**, choose `main` and `/ (root)`, then save.

Expected: GitHub reports that the site is being built from `main`.

- [ ] **Step 3: Wait for the deployment to complete**

Check the repository's Pages settings or Actions deployment status until it reports success.

Expected: the Pages deployment is marked successful and the public URL is shown.

- [ ] **Step 4: Verify the public response**

Run:

```bash
curl --fail --silent --show-error https://minowaoyaji.github.io/minowaoyaji_general/ | python3 -c 'import sys; p=sys.stdin.read(); assert "<div>test</div>" in p; assert "<div>test2</div>" in p'
```

Expected: exit status 0 with no output.

- [ ] **Step 5: Verify repository state**

Run:

```bash
git status --short --branch
```

Expected: `main` is synchronized with `origin/main` and there are no uncommitted changes.
