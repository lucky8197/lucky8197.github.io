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
work-sky.html         资讯类 App · 四端交付案例（无截图，保密）
work-trackmap.html    轨迹记录生成器 · 行程海报 App
work-dungeon.html     像素地牢冒险 · Godot 2D
work-birds.html       愤怒的小鸟 · Godot 2D 物理游戏
work-qt.html          Qt 鸿蒙化适配 · OpenHarmony
assets/               项目截图（480px 宽 JPEG，首页缩略图与详情页共用）
assets/video/         项目录屏（H.264 MP4 + 同名 JPG 封面）
robots.txt            爬虫规则
sitemap.xml           站点地图（首页 + 10 个详情页）
.nojekyll             跳过 Jekyll 处理，直接静态托管
```

## 视频规范

录屏统一放在 `assets/video/`，命名 `<项目名>.mp4`，并生成同名 `<项目名>.jpg` 作封面（`<video poster="...">`）。
没有封面时浏览器会停在第一帧，若首帧是黑场就会显示成黑框。

转码命令（H.264 + faststart + 静音，30fps）：

```bash
ffmpeg -i 原视频.mp4 -c:v libx264 -preset slow -crf 30 -profile:v main \
  -pix_fmt yuv420p -r 30 -movflags +faststart -an 输出.mp4
```

**上传前务必检查画面里的隐私信息**：手机号、真实账号、服务器 IP、浏览器地址栏。必要时用局部模糊：

```bash
ffmpeg -i in.mp4 -filter_complex \
 "[0:v]crop=W:H:X:Y,scale=540:-2[base];[base]split[b1][b2];\
  [b2]crop=w:h:x:y,gblur=sigma=14[bl];[b1][bl]overlay=x:y[v]" -map "[v]" ... out.mp4
```

已接入的视频：轨迹记录生成器、像素地牢、愤怒的小鸟、PriceWatch 面板。

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
