# lightforever.cn → Hugo + GitHub Pages 完整迁移进度

**最后更新**：2026-04-29
**状态**：全站已部署到 GitHub Pages，Giscus 评论已启用，4 轮视觉/性能优化完成，README/CLAUDE.md/PROGRESS.md 三件套齐全（150 页，主页 0 外部阻塞资源）

> **位置说明**：本文件原本在工作目录 `D:/AIAgents/lightforever-blog/PROGRESS.md`（仓库外，仅本地工作笔记）。后来一并搬进了 `blog/` 仓库根目录，所以下文路径已改为相对仓库根的形式。
>
> 迁移脚本 `convert2.py` / `scan_images.py` / `crawl/` 数据集仍只在工作目录上一层，**没有放进 git 仓库**——文中提到时按代码字体显示而非链接。

---

## ✅ 已完成（第二轮：完整迁移）

### 内容覆盖
- **文章**：46 篇（原站 48 篇中 2 篇作为 page 迁移）
- **页面**：14 个（含聚合页 4 个 + 独立页 10 个）
- **图片**：27 张本地化（wp-content/uploads 原路径保留 + 外部图床 raw.githubusercontent/gitee 下载到 `/img/external/...`）

### 分类统计（与原站对齐）
| 分类 | 原站 | 本地 |
|---|---|---|
| 课程测评 | 23 | 23 |
| 随感 | 14 | 14 |
| 课程笔记 | 4 | 4 |
| cs | 5 | 5 |
| physics | 1 | 1 |

### 数据来源与脚本
- **`convert2.py`**（仓库外）— 通过 WordPress REST API（`/wp-json/wp/v2/posts`、`/pages`、`/media`、`/categories`、`/tags`）拉取完整元数据，然后：
  - `content.rendered` → 清理 Typora MathJax（保留 `$...$` 源码 / 删除 SVG）
  - 删除 Gutentor 文章列表块（聚合列表），保留 Gutentor 图片块
  - 下载所有图片到 `/static/img/`，重写 `<img src>` 为本地路径
  - pandoc 转 Markdown + 后处理（修复公式里的 `\_`、`&lt;` 转义）
  - 按原 slug（URL-decode 去中文标点）生成 Hugo front matter
- **`scan_images.py`**（仓库外）— 扫描生成的 Markdown 里仍指向外部的图片（最终结果：0）
- **`crawl/listing/`**（仓库外）— WordPress REST API 的原始 JSON 数据

### 聚合页（手写列表，对应原 WordPress Gutentor 自动列表）
- **课程测评**（`/evaluation/`）按大一上/下、大二上三学期分组
- **课程笔记**（`/course-notes/`）
- **notes**（`/notes/`）物理 + cs 技术笔记
- **随感录**（`/thoughts/`）14 篇时间倒序

### 主页视觉（`layouts/index.html` 覆盖）
- 头像：原站 `53c268684...png` 下载后放到 `assets/img/avatar-home.png`（Stack 主题通过 `.Resources.Get` 读取）
- sidebar 标题 "World of Dreams" + 原站介绍 "最近决定自己做一个个人博客..."
- 4 个介绍卡片（关于课程测评 / 关于我的笔记 / 关于随感录 / 向我提问），2×2 网格，鼠标悬浮上浮
- 下方文章列表（分页 10 条/页）

### 样式
- [assets/scss/custom.scss](assets/scss/custom.scss) — 蓝白配色 + PingFang SC / 微软雅黑 CJK 字体 + 主页卡片样式 + 图片居中

### 菜单
- 主页 / 写在前面 / 关于作者 / 随感录 / 课程测评 / 课程笔记 / notes / 一些资料 — 8 项，已链到新聚合页

### 部署
- [.github/workflows/hugo.yml](.github/workflows/hugo.yml) — Hugo Extended 0.160.1 + GitHub Pages

### 构建验证
- `hugo` → **Pages: 149, Paginator: 15, Aliases: 43, 0 errors**
- 全部 104 条 sitemap URL 批量 HEAD 请求：**OK 104 / FAIL 0**

---

## 🚀 第三轮：性能与视觉优化（2026-04-22）

用户反馈三个问题 → 全部修复：

### 1. 首页 4 张介绍卡片字太小
- **根因**：Stack 主题用 `html { font-size: 62.5% }`（1rem = 10px），之前写的 `1.15rem` 实际只渲染成 11.5px。
- **修复**：[assets/scss/custom.scss](assets/scss/custom.scss) 完全重写 `.home-intro-cards`，按 rem=10px 校准：标题 1.9rem (19px)，正文 1.5rem (15px)，emoji 图标 3.2rem (32px)，卡片 padding 2rem。
- **布局升级**（[layouts/index.html](layouts/index.html)）：每张卡片左侧加 emoji 图标（📚📝💭💌），悬浮显示左侧蓝色装饰条 + 标题变色，三行文字省略号统一高度。

### 2. 网站加载慢（每页都慢）
- **真正根因**：Stack 主题默认从 `fonts.googleapis.com` 加载 Lato 字体——**中国大陆 GFW 阻塞**，每页等待数秒超时后才渲染。另外图片 `image-2-4.jpg` 有 1.8MB。
- **修复 A**：[layouts/_partials/head/custom-font.html](layouts/_partials/head/custom-font.html) 空覆盖主题的 Google Fonts partial，完全禁用外部字体加载。用 `custom.scss` 里的 PingFang SC / 微软雅黑系统字体替代。
- **修复 B**：[data/external.toml](data/external.toml) 覆盖 KaTeX / PhotoSwipe CDN，从 jsdelivr 换到阿里云 `registry.npmmirror.com`（国内直连）。
- **修复 C**：图片压缩（JPEG quality 82 + 最大边 1600px）：
  - `image-2-4.jpg`: 1.78MB → 144KB
  - `9833f3b6...jpg`: 362K → 163K
  - `IMG_20201230_161114.jpg`: 347K → 120K
  - `lake-669911_1920.jpg`: 311K → 260K
  - 合计 public/ 从 ~7MB 降到 5.3MB
- **修复 D**：[hugo.yaml](hugo.yaml) 加 `minify.minifyOutput: true`，Hugo 构建用 `hugo --minify`，index.html 从 22KB → 15KB。
- **修复 E**：Giscus `comments.enabled: false`（占位符 repoID 会发无效请求），配好真实 ID 后再打开。
- **验证**：curl 主页 Response 无任何 `googleapis.com` / `jsdelivr.net` 引用，本地回环响应 < 2ms。

### 3. 头像显示为竖椭圆形
- **根因**：原 `avatar-home.png` 尺寸 320×219（非正方形），被主题容器强制拉伸 + `border-radius: 50%` 得到椭圆。
- **修复**：[assets/img/avatar-home.png](assets/img/avatar-home.png) 替换为原站真正的头像文件 `2940e1441f49fcf589a0986c05200f9-300x300.jpg` 缩放到 **256×256** PNG。并在 `custom.scss` 加 `.site-logo { object-fit: cover; aspect-ratio: 1/1 }` 防御。

---

## 🚀 第四轮：首页底部封面图 + favicon + footer 微调（2026-04-26）

### 1. 全套 favicon
- [layouts/_partials/head/custom.html](layouts/_partials/head/custom.html) 加 favicon-16/32/96/192 + apple-touch-icon-180，对应 `static/` 根目录的 PNG，提升 iOS 主屏 / Android 添加到桌面 / 老浏览器兼容。

### 2. 封面图从全站底部 → 仅主页底部
- **问题**：把封面图放在 `footer/custom.html` 会让每篇文章末尾都被一张大图打断阅读节奏。
- **修复**：[layouts/_partials/footer/custom.html](layouts/_partials/footer/custom.html) 清空。改在 [layouts/index.html](layouts/index.html) 主页结尾加 `.home-cover` 区块（带 `<figcaption>— Let the Light Forever —</figcaption>` 署名）。
- **视觉升级**（[assets/scss/custom.scss](assets/scss/custom.scss) `.home-cover`）：
  - 宽度从 960px → 720px（更精致）
  - 加 radial-gradient mask 让边缘自然融入背景
  - 图下方加灰色斜体 caption

### 3. Giscus 评论正式启用
- [hugo.yaml](hugo.yaml) `params.comments.enabled: true`，repo/repoID/category/categoryID 全部填入用户提供的真实值。
- 验证：build 后 `public/{文章页, page 页}/index.html` 都包含 `https://giscus.app/client.js` 引用与 `data-repo=Light-Forever/Light-Forever.github.io`、`data-repo-id=R_kgDOSMYzbQ` 等属性。主页 index.html 不含评论（合理）。
- light/dark 跟随 Stack 主题颜色切换（Stack 主题自带 `setGiscusTheme` 监听 `onColorSchemeChange` 事件）。

### 4. 部署
- GitHub 仓库：[Light-Forever/Light-Forever.github.io](https://github.com/Light-Forever/Light-Forever.github.io)
- 已通过 GitHub Actions（[hugo.yml](.github/workflows/hugo.yml)）部署到 https://Light-Forever.github.io/
- 已 commit 历史：
  - `8ab909d` 初始化 Hugo 博客
  - `84ef006` 启用 Giscus 评论 + 添加 .gitignore
  - `6514d6d` 添加 favicon、修复侧边栏 mail 图标、加全站底部封面图

---

## ⏳ 仍待用户手动完成

### 1. 提交并推送本轮改动（封面图改为仅首页）
本地仍有 3 个未提交改动（把封面图从全站底部移到只在首页底部）：
```bash
cd D:/AIAgents/lightforever-blog/blog
git add assets/scss/custom.scss layouts/_partials/footer/custom.html layouts/index.html
git commit -m "封面图改为仅在首页底部，其他页面恢复纯净"
git push
```
推送后 GitHub Actions 会自动重新部署。

### 2.（可选）保留原域名 lightforever.cn
- DNS 加 CNAME：`www` → `Light-Forever.github.io`
- 新建 [static/CNAME](static/CNAME)，内容 `www.lightforever.cn`
- 仓库 Settings → Pages → 自定义域名填 `www.lightforever.cn`，勾选 Enforce HTTPS
- 同时把 hugo.yaml 的 `baseurl` 改回 `https://www.lightforever.cn/`

### 3.（可选）后续可改进项
- 「一些资料」页：原站有密码保护的电子书下载链接未迁移，需要补上
- 电子书集合 / 向我提问 / Contact 等次要页内容已迁移但未放主菜单

---

## 🧪 本地预览

```bash
cd D:/AIAgents/lightforever-blog/blog
hugo server
# 浏览器打开 http://localhost:1313
```

关键页面：
- 主页 http://localhost:1313/
- 课程测评 http://localhost:1313/evaluation/
- 随感录 http://localhost:1313/thoughts/
- 课程笔记 http://localhost:1313/course-notes/
- notes http://localhost:1313/notes/
- 物理笔记（含公式）http://localhost:1313/2021/04/23/a-brief-summary-of-chapter-7-mean-field-theory-of-phase-transitions/

---

## 📁 关键文件位置

```
D:/AIAgents/lightforever-blog/         ← 本地工作目录（不在 git 里）
├── convert2.py                        ← 全站迁移脚本（WordPress REST API → Hugo）
├── scan_images.py                     ← 扫描外部图片引用
├── crawl/                             ← 原始抓取数据
│   ├── www.lightforever.cn/           ← wget 原始镜像
│   ├── missing/                       ← curl 补抓的中文 slug HTML
│   └── listing/                       ← REST API JSON（posts / pages / media / cats / tags / sitemap）
└── blog/                              ← Hugo 项目（= GitHub 仓库根，推送到 GitHub）
    ├── README.md                      ← 网站说明（用户亲手书写的随感《在AI时代留下一点自己的痕迹》）
    ├── CLAUDE.md                      ← 技术架构 + 接力说明，给未来的我和未来的 Claude
    ├── PROGRESS.md                    ← 本文件，完整迁移过程记录
    ├── hugo.yaml
    ├── .github/workflows/hugo.yml
    ├── assets/
    │   ├── scss/custom.scss
    │   └── img/avatar-home.png        ← 侧边栏头像（原站人像）
    ├── layouts/
    │   ├── index.html                 ← 主页定制（4 张介绍卡片 + 文章列表 + 排版式署名）
    │   └── shortcodes/{netease,fixme}.html
    ├── static/img/                    ← 23 张下载的图片
    │   ├── 2019/ 2021/ 2022/          ← 原站 wp-content/uploads 镜像
    │   ├── avatar-home.png
    │   └── external/                  ← raw.githubusercontent / gitee 图床
    ├── themes/stack/                  ← submodule
    └── content/
        ├── _index.md              ← 主页（仅 title）
        ├── post/                  ← 46 篇文章（中文 slug）
        ├── page/                  ← 14 个页面
        │   ├── evaluation/        ← 课程测评聚合页
        │   ├── course-notes/
        │   ├── notes/
        │   ├── thoughts/
        │   ├── about/ preface/ resources/
        │   ├── contact/ wechat/ ebooks/ links/ question/ photograph/
        │   └── privacy-policy/
        ├── search.md
        └── archives/_index.md
```

---

## 🎯 关键设计决策

1. **数据源**：从 REST API 的 `content.rendered` 提取，比 wget 的 HTML `entry-content` 干净得多——不需要剥离侧边栏、导航、评论组件。
2. **slug 策略**：URL-decode 原 slug 为中文，然后去除中文标点（与 Hugo 自动 URL sanitization 一致），保证 front matter slug = 实际生成路径。URL 与原站 `/2021/01/27/<中文>/` 100% 兼容。
3. **聚合页**：原站用 Gutentor 插件自动生成的"课程测评"等列表在迁移后改为手写 Markdown 列表（按学期分组），更干净且易维护。
4. **主页视觉还原**：通过覆盖 `layouts/index.html`，在文章列表上方加入 4 张原站风格的介绍卡片，保留 Stack 主题的文章卡片列表。
5. **图片本地化**：所有外部图床（原域名 + raw.githubusercontent + gitee）都下载到 `/static/img/`，不再依赖外部服务。

---

## ⚠ 已知限制 / 保留项

- **baseurl / Giscus 字段**：仍是占位符，部署前必须替换
- **一些资料页**：原站有密码保护的电子书下载链接未迁移；保留了页面文字内容，补链接需要用户手动完成
- **电子书集合 / 向我提问 / Contact 等次要页**：内容已迁移但未放入主菜单，需要时可加
