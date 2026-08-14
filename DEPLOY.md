# WKing 单文件静态站点 · 部署指南

本目录 `index.html` 是一个**零依赖、零构建**的单文件静态网页：HTML / CSS / JavaScript 全部内联，双击即可在浏览器打开，也能直接托管到任意静态平台公开访问。

## 文件清单
- `index.html` —— 主站点（部署用入口文件，完整内联，约 99 KB）
- `reports/` —— 四份 PPT 式周报（相对路径引用，随站点一起上传即可）
- `overview-2026-08-17.md` —— 交付说明

## 部署前必做（已完成 ✅）
- 已将 `index.html` 中占位域名 `wking.example.com` 替换为实际 GitHub Pages 地址 `https://wking-jj.github.io/WKing/`（canonical / OG / JSON-LD 已同步）。
- 若之后改用自定义域名，只需把上述地址改为你的域名即可。

## 方式一：GitHub Pages（推荐，免费，保姆级）

> 你的账号信息已写死：**用户名 `WKing-JJ`**、**仓库名 `WKing`**、**公开网址 `https://wking-jj.github.io/WKing/`**。
> 下面每一步都标了"点哪里 / 填什么 / 注意什么"，跟着点就行。
> 💡 **怕敲命令？直接跳到下方「零命令图形界面版：用 GitHub Desktop」**，全程鼠标点，不用输任何命令。

### 第①步：在 GitHub 新建仓库（网页操作）
1. 打开浏览器，登录 <https://github.com>（用 `WKing-JJ` 账户）。
2. 右上角头像左侧有个 **＋（加号）** 图标 → 点它 → 选 **New repository（新建仓库）**。
3. 进入新建页面，按下面填：
   - **Repository name（仓库名）**：填 `WKing`（必须一模一样，网址才是 `wking-jj.github.io/WKing`）。
   - **Description（描述）**：可留空，或填"WKing 个人资讯站"。
   - **Public / Private**：务必选 **Public（公开）**——Pages 免费托管只支持公开仓库。
   - ⚠️ **Important（重要）**：下方三个勾选框 **Initialize this repository with（初始化）** 区域里的
     - ☐ Add a README file
     - ☐ Add .gitignore
     - ☐ Choose a license
     这三项 **全部不要勾**（我们的本地仓库已经有文件，勾了会冲突导致推不上去）。
4. 点最下方的绿色按钮 **Create repository（创建仓库）**。
5. 创建成功后会进入一个空仓库页面（显示"quick setup"之类），**不用管它上面的命令**，直接进行第②步。

### 第②步：生成访问令牌 PAT（只需做一次）
`git push` 时"密码"那栏要填的不是你的 GitHub 登录密码，而是一串 **Personal Access Token（个人访问令牌，简称 PAT）**。
1. 点 GitHub 右上角**头像** → **Settings（设置）**。
2. 左侧最下方 **Developer settings（开发者设置）** → **Personal access tokens** → **Tokens (classic)**。
3. 点 **Generate new token（生成新令牌）** → 再点 **Generate new token (classic)**。
4. 填写表单：
   - **Note（备注）**：填 `wking-push`（随便记，方便认）。
   - **Expiration（过期时间）**：选 **90 days**（90 天）或 **No expiration（不过期）** 都行；选不过期的话以后不用重做这步。
   - **Select scopes（权限勾选）**：找到 **`repo`** 这一大项，把它的复选框 **勾上（包含下面所有子项）**。这是推送代码必需的最小权限。
   - 其余权限**不用勾**。
5. 页面最底部点绿色 **Generate token（生成令牌）**。
6. 生成后会显示一长串 **`ghp_xxxxxxxxxxxxxxxx`** 的字符——**这是唯一一次显示机会，立刻复制保存好**（可先粘到记事本）。如果丢了只能重新生成一个。

### 第③步：把本地代码推送到 GitHub（在你自己电脑上执行）
> 注意：下面命令要在**你自己的 Windows 电脑**上跑（我们目前的运行环境连不上 github.com，必须由你的电脑出网）。

**方式 A：用 Git Bash（推荐新手）**
1. 打开 **Git Bash**（装了 Git 就有；开始菜单搜 "Git Bash"）。
2. 进入站点目录，逐行粘贴执行：
   ```bash
   cd /d/wangrlly/Documents/wordbuddy/wking-site
   git push -u origin main
   ```
3. 第一次推送会弹出登录框：
   - **Username（用户名）**：填 `WKing-JJ`
   - **Password（密码）**：**粘贴第②步复制的 PAT（`ghp_...` 那串）**，不是你的账户密码！
   - 提示：Git Bash 里粘贴是 **右键 → Paste**（或 Shift+Insert）；输入密码时屏幕**不会显示任何字符**，这是正常的，粘完直接回车。
4. 看到类似 `Enumerating objects...` `To https://github.com/WKing-JJ/WKing.git` `branch 'main' set up to track 'origin/main'` 和 `done.` 就成功了。

**方式 B：用 PowerShell / 终端（如果 Git Bash 没有）**
1. 打开 **PowerShell**（开始菜单搜 PowerShell）。
2. 逐行执行：
   ```powershell
   cd D:\wangrlly\Documents\wordbuddy\wking-site
   git push -u origin main
   ```
3. 弹窗（或命令行）要求登录时，用户名填 `WKing-JJ`，密码填 **PAT（不是账户密码）**。
4. 若弹出的是 GitHub 网页登录窗口：用 `WKing-JJ` 登录即可，登录成功会自动继续推送。

**常见失败与处理**
- ❌ `remote: Repository not found` / `could not read Username`：仓库还没建好（先回第①步），或仓库名/用户名拼错（应为 `WKing-JJ/WKing`）。
- ❌ `Permission denied (403)`：密码栏填成了账户密码，或 PAT 没勾 `repo` 权限——重做第②步生成 PAT。
- ❌ `failed to resolve host` / 一直转圈：电脑没联网，或公司网络屏蔽了 github.com。
- ❌ `Updates were rejected because the remote contains work`：你建仓库时勾了 README 等文件——删掉重建成空仓库（第①步），再推。

### 第④步：开启 GitHub Pages（网页操作）
1. 推送成功后，打开仓库页面 <https://github.com/WKing-JJ/WKing>。
2. 点仓库顶部导航栏的 **Settings（设置）**（最右侧齿轮图标）。
3. 左侧菜单找 **Pages**（可能在 "Code and automation" 分组下，往下滚）。
4. 在 **Build and deployment** 区域：
   - **Source（来源）**：选 **Deploy from a branch（从分支部署）**。
   - **Branch（分支）**：点下拉选 **`main`**（我们用的就是 main）。
   - **Directory（目录）**：选 **`/ (root)`**（根目录，因为 `index.html` 在根）。
5. 点 **Save（保存）**。
6. 页面会出现一行提示："Your site is being built..."（正在构建）。**等约 1 分钟**（首次可能 1–3 分钟）。
7. 回到 **Settings → Pages**，顶部会显示绿色对勾 + 你的公开网址：
   **https://wking-jj.github.io/WKing/**
8. 浏览器打开这个网址，就能看到 WKing 站点了 🎉。

### 第⑤步：以后怎么更新
改完内容（比如改了 `index.html`）后，只需在你电脑的该目录执行三行：
```bash
git add -A
git commit -m "更新说明"
git push
```
GitHub Pages 会自动重新发布，**不用再进设置**。大约 1 分钟后刷新网址即可看到新内容。
（注意：`git push` 的 PAT 在 Windows 上通常会被凭据管理器记住一段时间，短期不用每次重填。）

> 若仓库名不是 `WKing` 而是别的，相对链接（`reports/...`、页内锚点）依然有效，无需改代码；只是网址会变成 `wking-jj.github.io/<你的仓库名>/`，同时记得同步改 `index.html` 里的域名与 `origin` 地址。

### 🖱️ 零命令图形界面版：用 GitHub Desktop（新手首选，不用敲任何命令）
如果你在上面的命令行步骤卡住了（打不开 Git Bash、路径报错、粘贴不生效等），**直接用 GitHub Desktop 即可**，全程鼠标点击：

1. **下载安装**：浏览器打开 <https://desktop.github.com/> → 点 **Download for Windows** → 双击安装包安装 → 打开后用 GitHub 账户 **`WKing-JJ`** 登录（按提示授权一次）。
2. **添加本地仓库**：顶部菜单 **File → Add Local Repository…**（中文：文件 → 添加本地仓库）→ 点 **Choose…**（选择…）→ 选中文件夹 **`D:\wangrlly\Documents\wordbuddy\wking-site`** → 点 **Add Repository**。
   - 这个文件夹我们已经初始化好 Git 仓库、也设好了远端 `origin`，Desktop 会直接识别，无需任何配置。
3. **推送上网**：界面左侧会列出你本地的 4 个提交。点击右上角的 **Publish branch**（发布分支）或 **Push origin**（推送）。
   - 若弹出"选择发布位置"：确认账户是 **`WKing-JJ`**、仓库名 **`WKing`**、可见性选 **Public**，再点 **Publish**。
4. 等进度条走完，打开 <https://github.com/WKing-JJ/WKing> 就能看到代码已经上去了。
5. 然后照常做 **第④步（Settings → Pages）** 开启网站即可（见上）。

> 以后更新：在 GitHub Desktop 里改完文件 → 左下角写一句摘要 → 点 **Commit to main** → 点 **Push origin**，网站自动更新，全程不用命令行。

### 命令行版排错（如果你仍想用命令）
- **打不开 Git Bash**：开始菜单搜 "Git Bash"；若搜不到，说明没装 Git → 去 <https://git-scm.com/> 下载安装（一路 Next），装完重开菜单即可。
- **路径报错 `cd: no such file`**：在 Git Bash 里必须用 **`/d/wangrlly/...`**（斜杠、盘符前加 `/`）；若你在 **PowerShell**，则用 **`D:\wangrlly\...`**（反斜杠）。两者语法不同，不要混用。
- **逐行执行的正确做法**：一次只粘**一行**并回车，不要两行一起粘。第一行 `cd ...` 回车后，再粘第二行 `git push ...` 回车。
- **push 要填的"密码"**：弹窗里用户名 `WKing-JJ`、**密码栏粘 PAT（`ghp_...`）不是账户密码**（见上"生成 PAT"一节）。

## 方式二：Vercel（零配置，免费）
1. 登录 vercel.com → **Add New → Project** → 导入含本目录的 Git 仓库；或直接拖拽本目录到 Vercel「Deploy」。
2. Framework Preset 选 **Other**，Build Command 留空，Output Directory 留空（默认读取 `index.html`）。
3. 点击 Deploy，数秒后得到 `https://<项目>.vercel.app/` 公开网址。
4. 后续推送自动触发重新部署。

## 方式三：Netlify / Cloudflare Pages
同上：拖拽目录或连接 Git，构建命令留空，发布目录留默认，即可获得公开网址。

## 本地预览（部署前自检）
- 直接双击 `index.html`；或起一个本地服务：`python3 -m http.server 8000`，浏览器开 `http://localhost:8000`。
- 检查：顶栏汉堡菜单（窄屏）、订阅表单保存提示、滚动进度条与回到顶部、底部"站点数据总览"。

## 注意事项
- 全站无任何外部 CDN / 网络请求，离线也能完整运行；统计与订阅偏好保存在浏览器 `localStorage`（本机生效，非服务器侧）。
- 如需真实邮件订阅/访问统计后端，再接入第三方服务即可，前端无需改动。
