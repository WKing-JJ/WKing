# WKing 单文件静态站点 · 部署指南

本目录 `index.html` 是一个**零依赖、零构建**的单文件静态网页：HTML / CSS / JavaScript 全部内联，双击即可在浏览器打开，也能直接托管到任意静态平台公开访问。

## 文件清单
- `index.html` —— 主站点（部署用入口文件，完整内联，约 99 KB）
- `reports/` —— 四份 PPT 式周报（相对路径引用，随站点一起上传即可）
- `overview-2026-08-17.md` —— 交付说明

## 部署前必做（1 处）
把 `index.html` 里的占位域名换成你的真实域名（否则分享卡片/SEO 会指向示例地址）：
- `<link rel="canonical" href="https://wking.example.com/">`
- `<meta property="og:...">` 与 JSON-LD 中的 `url` 字段
- 如不需要，也可保留占位，不影响页面正常运行。

## 方式一：GitHub Pages（推荐，免费）
1. 在 GitHub 新建仓库（如 `wking`），把本目录全部内容推送为仓库根。
2. 仓库 **Settings → Pages → Build and deployment → Source** 选 **Deploy from a branch**。
3. Branch 选 `main` / `master`，目录选 `/ (root)`，保存。
4. 约 1 分钟后访问 `https://<用户名>.github.io/<仓库名>/`。
5. 之后每次 `git push` 即自动更新（无需构建）。

> 若仓库名不是 `wking`，相对链接（`reports/...`、页内锚点）依然有效，无需改动。

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
