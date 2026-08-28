# 期权工作台 · Options Lab

一个零依赖的单页期权学习站点：从合约要素讲到 19 种组合结构，所有损益图、希腊字母曲线和计算器都在浏览器里实时渲染。

线上地址：部署后补充。

## 内容结构

| 锚点 | 章节 | 说明 |
| --- | --- | --- |
| `#basics` | 基础 | 期权到底是什么：合约要素、权利义务、内在价值与时间价值 |
| `#greeks` | 希腊字母 | Delta / Gamma / Theta / Vega / Rho 五个方向盘 |
| `#lab` | 损益实验室 | 自由拼腿，实时画到期与当前损益曲线 |
| `#strategies` | 策略库 | 19 种结构的形态、适用行情与风险特征 |
| `#cc` | 备兑手册 | 备兑开仓实操：年化收益、被行权价与保本点计算器 |
| `#risk` | 风险 | 常见亏损来源与开仓前检查清单 |
| `#cases` | 案例 | 完整案例从开仓走到平仓 |
| `#quiz` | 自测 | 选择题与解析 |

## 技术说明

- 纯静态：单个 `index.html`，内联 CSS 与 JavaScript，无外部 CDN、无图片、无字体请求。
- 无构建步骤：不需要 Node、不需要打包器，克隆下来直接就能跑。
- 损益图使用原生 Canvas 绘制，期权定价用内置的 Black–Scholes 实现。

## 本地预览

直接用浏览器打开 `index.html` 即可。若想用本地服务器（避免个别浏览器对本地文件的限制）：

```bash
python3 -m http.server 8000
# 然后访问 http://localhost:8000
```

## 部署到 Vercel

### 方式一：从 GitHub 导入（推荐）

1. 打开 [vercel.com/new](https://vercel.com/new)，选择 `options-learning` 这个仓库并点击 **Import**。
2. 配置保持默认即可：
   - **Framework Preset**：`Other`
   - **Root Directory**：`./`
   - **Build Command**：留空（本项目无需构建）
   - **Output Directory**：留空（默认使用仓库根目录）
3. 点击 **Deploy**。首次部署约十几秒，完成后会拿到一个 `*.vercel.app` 域名。

之后每次向默认分支推送都会自动触发生产环境部署，向其他分支推送会生成预览部署。

### 方式二：Vercel CLI

```bash
npm i -g vercel
vercel          # 预览部署
vercel --prod   # 生产部署
```

### 绑定自定义域名

在 Vercel 项目的 **Settings → Domains** 添加域名，然后按提示在域名服务商处配置 DNS：根域名加 `A` 记录指向 `76.76.21.21`，子域名加 `CNAME` 记录指向 `cname.vercel-dns.com`。

## 仓库文件

```
.
├── index.html    # 站点全部内容
├── vercel.json   # Vercel 配置：干净 URL + HTML 不做长缓存
├── .gitignore
└── README.md
```

`vercel.json` 里把 `index.html` 的 `Cache-Control` 设为 `must-revalidate`，这样每次重新部署后访问者都能立刻看到最新版本，而不会读到 CDN 里的旧缓存。
