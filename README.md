# 药企投递追踪助手：公开部署包

这个目录可用于发布一个任何人都能打开的静态 HTTPS 网页。页面不会把投递信息发送到 GitHub 或其他服务器；每位访问者的数据都保存在其浏览器当前网站来源的 localStorage 中。

## 发布前保护现有记录

你现在通过 `file://` 打开的网页，其记录与新 HTTPS 网站的存储彼此隔离。请先在当前网页导出个人 JSON 备份。发布后在新网址中导入备份，之后记录会保存在该浏览器的新网址下。不要把个人 JSON 备份上传到代码仓库。

## 用 GitHub Pages 发布

1. 在 GitHub 创建一个新仓库。若使用 GitHub Free，仓库需要公开；网页和仓库中的源码会公开，确认部署包中没有个人记录。
2. 把本目录中的 `site` 文件夹、`.github` 文件夹及本说明上传到仓库根目录。文件夹结构必须保持：`site/index.html`、`site/.nojekyll`、`.github/workflows/deploy.yml`。
3. 在仓库的 **Settings → Pages → Build and deployment** 中将 **Source** 设为 **GitHub Actions**。
4. 在 **Actions** 页面等待 `Deploy personal tracker to GitHub Pages` 完成。
5. 发布完成后，在 **Settings → Pages** 或该次 Actions 运行摘要中复制页面地址。将这个 HTTPS 链接分享给使用者。

之后更新仓库中的 `site/index.html` 并提交到 `main`，GitHub Actions 会自动发布新版本。

## 数据隔离说明

- 相同 HTTPS 地址在不同设备、不同浏览器或不同浏览器配置文件中，各有各的本地数据。
- 同一设备、同一浏览器配置文件、同一网址下打开多个标签页，会看到同一份数据。这是浏览器本地存储的正常行为。
- 换设备、换浏览器配置文件、清除网站数据或更换域名后，数据不会自动迁移；使用页面内导出/导入功能迁移。
- 本部署配置只发布 `site` 目录，不上传用户浏览器数据。
