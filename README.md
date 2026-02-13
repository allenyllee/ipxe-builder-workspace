# Workspace Layout

這個上層 repo 用 submodule 管理兩個子 repo：

- `ipxe-builder-app/`：前端 + Cloudflare Worker（對外服務）
- `ipxe-builder-template/`：給使用者 fork 的模板 repo（只負責 build）

## 目前狀態

- 上層已建立 submodule（見 `.gitmodules`）
- 子 repo 已各自有初始 commit（branch: `main`）

## 下一步：綁定 GitHub 並 push

### 1) 設定子 repo remote

```bash
git -C ipxe-builder-app remote add origin git@github.com:<you>/ipxe-builder-app.git
git -C ipxe-builder-template remote add origin git@github.com:<you>/ipxe-builder-template.git
```

### 2) push 子 repo

```bash
git -C ipxe-builder-app push -u origin main
git -C ipxe-builder-template push -u origin main
```

### 3) 把 submodule URL 改成 GitHub URL（很重要）

```bash
git submodule set-url ipxe-builder-app git@github.com:<you>/ipxe-builder-app.git
git submodule set-url ipxe-builder-template git@github.com:<you>/ipxe-builder-template.git
```

### 4) commit 上層 repo

```bash
git add .gitmodules ipxe-builder-app ipxe-builder-template README.md
git commit -m "manage app/template as submodules"
```

## 連動設定

在 `ipxe-builder-app/worker/wrangler.toml` 設定：

- `TEMPLATE_OWNER=<your-github-user-or-org>`
- `TEMPLATE_REPO=ipxe-builder-template`
- `TEMPLATE_BRANCH=main`
