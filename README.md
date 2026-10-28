# lucky8197.github.io

个人作品集站点，托管在 GitHub Pages：**https://lucky8197.github.io/**

纯静态 HTML + 内联 CSS，无框架、无构建、无 CI。改完 `git push` 到 `main`，约 30 秒后自动生效。

## 结构

```
index.html            首页：简介 + 项目卡片列表
work-paixue.html      排课侠 · 微信小程序
work-game.html        暗能共鸣 · 微信小游戏
work-spotdiff.html    找不同闯关 · H5 活动游戏
work-quiz.html        答题测算 · 知识闯关活动
work-pricewatch.html  盯价 PriceWatch · 价格库存监控
work-qt.html          Qt 鸿蒙化适配 · OpenHarmony
assets/               项目截图（480px 宽 JPEG，首页缩略图与详情页共用）
robots.txt            爬虫规则
sitemap.xml           站点地图（首页 + 6 个详情页）
.nojekyll             跳过 Jekyll 处理，直接静态托管
```

## 怎么改

- **改文字**：直接改对应 HTML 里的中文内容。
- **加一个项目**：复制 `index.html` 里一整块 `<article class="card">`，粘到 `.projects` 内；再复制任一 `work-*.html` 改内容，作为详情页。
- **加技能标签**：复制 `<ul>` 里的一项 `<li>`。
- **加截图**：图片放到 `assets/`，宽度统一 480px、JPEG 渐进式压缩，首页缩略图直接复用同一文件（CSS 缩到 104px）。
- **改完记得**：新的详情页要补进 `sitemap.xml`。

### 两个必须注意的坑

1. **只要 `<img>` 上写了 `width`/`height` 属性，CSS 就必须两个都显式覆盖。** 只覆盖 `width` 会让 HTML 的 `height` 继续生效，图片静默变形。
2. **改文案前先确认口径。** 对外统一用英文名 `Liang Luo`，头像缩写 `LL`；涉密或受甲方保密约束的项目不上公开页面；电话不写入页面，邮箱已公开。

## 本地预览与验证

直接双击 `index.html` 即可。验证布局用无头 Chrome 截图，比读源码推断可靠：

```bash
"C:/Program Files/Google/Chrome/Application/chrome.exe" --headless=new --disable-gpu --no-sandbox \
  --hide-scrollbars --window-size=1200,1400 --virtual-time-budget=8000 \
  --screenshot="out.png" "file:///<repo>/index.html"
```

## 部署环境说明

本机 `github.com:443` 不通，push 走 `ssh.github.com:443`（已配在 `~/.ssh/config`）。**不要用 `git pull --rebase`**，本机上会摧毁 `.git` 目录，改用 `git merge`。
