# 写给未来的我（以及未来的某个 Claude）

这个文件是 [World of Dreams](./README.md) 这个博客仓库的"操作手册兼记忆传承"。

如果你（未来的我）某天换了台设备，clone 下来发现"咦这是什么"；
或者你（未来的某个版本的 Claude）被请来接着改这个站——
下面这些是当时迁移时定下来的所有重要决策，看完应该就能马上接着写了 (^_^)v

---

## 现在的技术架构

| 项目 | 选型 | 备注 |
|---|---|---|
| 静态站生成 | **Hugo Extended 0.160.1** | 必须是 Extended 版（要 SCSS） |
| 主题 | [hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack) | 通过 git submodule 引入 |
| 部署 | GitHub Actions → GitHub Pages | 推 main 分支自动触发 |
| 评论 | **Giscus**（基于本仓库的 Discussions） | repo: `Light-Forever/Light-Forever.github.io` |
| 数学公式 | KaTeX | CDN 走 npmmirror，国内直连 |
| 字体 | 系统字体（PingFang SC / 微软雅黑） | 不再依赖 Google Fonts |
| 配色 | 蓝白主题（蓝 `#3b82f6`） | 深浅模式都已适配 |

## 仓库结构

```
blog/                              ← 这个仓库
├── hugo.yaml                      ← 全站配置：菜单、Giscus、widgets、permalinks…
├── .github/workflows/hugo.yml     ← GitHub Actions 自动部署
├── assets/
│   ├── scss/custom.scss           ← 所有视觉定制都在这一个文件（蓝白主题、卡片、署名…）
│   └── img/avatar-home.png        ← 侧边栏头像（256×256）
├── layouts/                       ← 主题覆盖层（site-level）
│   ├── index.html                 ← 主页：4 张入口卡片 + 文章列表 + 底部排版式署名
│   ├── _partials/head/custom.html       ← favicon
│   ├── _partials/head/custom-font.html  ← 空文件，用来禁用 Stack 的 Google Fonts
│   ├── _partials/footer/custom.html     ← 留空（封面图改去主页了）
│   └── shortcodes/{netease,fixme}.html
├── data/external.toml             ← 覆盖 KaTeX / PhotoSwipe CDN 走 npmmirror
├── content/
│   ├── _index.md                  ← 主页（仅 title）
│   ├── post/                      ← 46 篇文章（中文 slug，与原站 URL 100% 兼容）
│   ├── page/                      ← 14 个独立页面
│   │   ├── evaluation/ course-notes/ notes/ thoughts/  ← 聚合页（手写列表）
│   │   ├── about/ preface/ resources/
│   │   └── question/ photograph/ contact/ ebooks/ links/ wechat/ privacy-policy/
│   └── archives/_index.md
├── static/
│   ├── favicon-*.png + apple-touch-icon.png
│   └── img/{2019,2021,2022,external}/   ← 所有图片本地化，没有外链
└── themes/stack/                  ← submodule，clone 时记得 --recurse-submodules
```

## 本地写作流（最常用的几条命令）

```bash
# 第一次拉下来（或新设备）—— 一定要带 --recurse-submodules，否则主题缺失
git clone --recurse-submodules https://github.com/Light-Forever/Light-Forever.github.io.git blog
cd blog

# 写一篇新随感
hugo new post/我的新文章/index.md
# 然后编辑 content/post/我的新文章/index.md，front matter 里改 title / date / categories

# 本地预览（带草稿）
hugo server -D
# 浏览器打开 http://localhost:1313

# 推上线（GitHub Actions 1-2 分钟后自动部署）
git add . && git commit -m "..." && git push
```

环境装一次：

```bash
# Windows
choco install hugo-extended
# macOS
brew install hugo
```

---

## 几个迁移时定下的关键决策（千万别再踩这些坑！）

### 1. Stack 主题用了 `html { font-size: 62.5% }`

所以 **1rem = 10px**。写 SCSS 的时候记得换算：想要 16px 写 `1.6rem`，想要 20px 写 `2rem`。
一开始没注意这个，导致主页卡片字小到只有 11.5px，看了好半天才反应过来 🙃。

### 2. 千万不要让主题加载 Google Fonts

Stack 主题默认从 `fonts.googleapis.com` 拉 Lato，国内 GFW 挡掉，每页要等数秒才渲染。
已经用 `layouts/_partials/head/custom-font.html`（空文件）覆盖禁用，**别手贱去删它**。
中文字体走 `custom.scss` 里的系统字体栈（PingFang SC / 微软雅黑）。

### 3. CDN 必须走 npmmirror

`data/external.toml` 把 jsdelivr 改成了阿里云镜像，否则 KaTeX、PhotoSwipe 加载也很慢。
如果某天阿里云镜像挂了，可以再换一个国内可达的（清华、华为云都行）。

### 4. 图片走 `static/img/`，路径不要改

保留了 WordPress 时代的路径（`/img/2021/01/xxx.jpg`），这样原文 markdown 里
`<img src>` 不用动。外部图床（raw.githubusercontent / gitee）的图都下载到了
`/static/img/external/`。

### 5. slug 用中文，URL 与原站完全兼容

permalinks 规则是 `/post/:year/:month/:day/:slug/`，与原 WordPress 站
`/2021/01/27/<中文标题>/` 100% 一致。**不要改这个规则**，否则全站旧链接全挂、
搜索引擎索引也会全部失效。

### 6. 首页底部不要再放大图

试过把封面图放 `footer/custom.html`，每页都出现，会打断阅读节奏；
也试过只在主页底部放大图，仍然太重。现在是排版式署名（左右渐隐细线 + 中间斜体小字
`Let the Light Forever`），干净得多。如果未来想换回小印章式图片，
`assets/scss/custom.scss` 里 `.home-signature` 那段附近有方案。

### 7. Giscus 评论已配好

仓库 Discussions 已开启，App 已装。如果换仓库，要去 <https://giscus.app> 重新拿
`repoID` 和 `categoryID` 填回 `hugo.yaml`。light/dark 主题会跟随站点切换
（Stack 主题自带 `setGiscusTheme` 监听）。

### 8. 不要提交 `public/` 和 `resources/`

`.gitignore` 已忽略，GitHub Actions 会现场重建。本地 `hugo` 跑出来的产物只是给自己看的。

---

## 完整迁移记录

如果想看完整迁移过程（怎么从 WordPress REST API 拉数据、pandoc 怎么用、
逐轮性能 / 视觉优化、踩过哪些坑），见同目录 [`PROGRESS.md`](./PROGRESS.md)。

迁移脚本本体（`convert2.py`、`scan_images.py`、原始 wget / REST API 抓回来的
JSON 数据）当时都在工作目录上一层，没有放进 git 仓库。如果要重跑迁移，
得先把那些文件再找回来。

---

## 给未来某个 Claude 的一段话

如果你正在读这份文件，意味着我（用户）请你接着改这个博客。几条建议：

1. **先读 [PROGRESS.md](./PROGRESS.md)** 的最后几节，能立刻 catch up 到现在的状态。
2. **改样式优先用 `assets/scss/custom.scss`**，不要去改 `themes/stack/` 里的任何东西
   （submodule 改了也会被覆盖）。要重写主题模板就在 `layouts/` 下覆盖。
3. **每次改完跑 `hugo --minify` 验证**，看看 `public/` 里关键页面（主页、一篇文章页、
   一个聚合页）的 HTML 渲染是否符合预期。
4. **不要主动 commit / push**，除非用户明确说"push it"。
5. **保留我的语气**：颜文字、`叭` `啦` 这种语气词、自嘲、跳跃感——不要写成正经
   博客的官话。

—— 祝你也写得开心 (\*/ω＼\*)
