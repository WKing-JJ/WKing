# WKing 资讯站

单文件静态资讯网站（**行业信息 / 管理技能 / 智能技术 / 设施技术** 四大板块），零依赖、零构建，可直接部署到 GitHub Pages 公开访问。

- `index.html` —— 主站点（HTML/CSS/JS 全部内联，双击即用，约 99 KB）
- `reports/` —— 四份 PPT 式周报（相对路径引用，随站点一起上传）
- `overview-2026-08-17.md` —— 交付说明
- `DEPLOY.md` —— 多平台部署指南

## 本地预览
直接双击 `index.html`；或起本地服务：

```bash
python3 -m http.server 8000
# 浏览器打开 http://localhost:8000
```

## 部署（GitHub Pages · 方式一）
本仓库按「从分支部署」配置，仓库根目录即站点根：

1. 在 GitHub 新建仓库（如 `wking`）。
2. 将本仓库设为远程：
   ```bash
   git remote add origin git@github.com:<用户名>/<仓库>.git
   # 或用 HTTPS：
   # git remote add origin https://github.com/<用户名>/<仓库>.git
   ```
3. 推送：
   ```bash
   git push -u origin main
   ```
4. 仓库 **Settings → Pages → Build and deployment → Source** 选 **Deploy from a branch**，Branch 选 `main`、目录选 `/ (root)`，保存。
5. 约 1 分钟后访问 `https://<用户名>.github.io/<仓库>/`，之后每次 `git push` 自动更新。

> 若使用自定义域名：在仓库根添加 `CNAME` 文件（仅写一行域名，如 `wking.com`），并在 DNS 处按 GitHub 指引配置。
> 部署前建议把 `index.html` 中 `wking.example.com` 占位域名替换为真实地址（canonical / OG / JSON-LD）。

## 说明
全站无外部 CDN / 网络请求，离线可完整运行；浏览/订阅统计保存在浏览器 `localStorage`（本机生效）。
