# Vibe Coding to Production

🇺🇸 [English](README.md) | 🇨🇳 [中文](README-zh.md) | 🇻🇳 [Tiếng Việt](README-vi.md) | 🇪🇸 [Español](README-es.md) | 🇩🇪 [Deutsch](README-de.md)

一份完整的分步指南，专为**非开发者**设计，教你使用 Claude Code 进行 AI 辅助编程（vibe coding），从零开始构建网站并部署到生产环境。

完成本指南后，你将拥有：

- 一个功能完整的 Next.js 网站
- Stripe 支付集成
- 使用 Dokploy 部署到线上服务器
- Google Analytics 追踪配置

无需任何编程经验。我们开始吧。

---

## 目录

1. [创建 GitHub 账户和仓库](#1-创建-github-账户和仓库)
2. [安装 Git、Node.js 和 Claude Code](#2-安装-gitnode-js-和-claude-code)
3. [克隆 GitHub 仓库](#3-克隆-github-仓库)
4. [配置 Claude Code](#4-配置-claude-code)
5. [使用 Next.js 构建网站](#5-使用-nextjs-构建网站)
6. [配置 Stripe 支付](#6-配置-stripe-支付)
7. [配置 DigitalOcean 服务器](#7-配置-digitalocean-服务器)
8. [安装和配置 Dokploy](#8-安装和配置-dokploy)
9. [部署网站](#9-部署网站)
10. [配置 Google Analytics](#10-配置-google-analytics)

---

## 1. 创建 GitHub 账户和仓库

GitHub 是你的网站代码的存储地方。把它想象成一个云端项目文件夹，同时还能追踪你所做的每一次修改。

### 创建 GitHub 账户

1. 访问 [github.com](https://github.com)
2. 点击 **Sign up**
3. 输入你的邮箱、创建密码并选择用户名
4. 完成验证并点击 **Create account**
5. 查收邮件并验证账户

### 创建新仓库

仓库（或称"repo"）就像 GitHub 上的项目文件夹。

1. 登录后，点击右上角的 **+** 图标
2. 点击 **New repository**
3. 填写详细信息：
   - **Repository name**：为你的项目选择一个名称（例如 `my-website`）
   - **Description**：可选，添加简短描述
   - **Public** 或 **Private**：如果不想让他人看到你的代码，选择 Private
   - 勾选 **Add a README file**
4. 点击 **Create repository**

<img width="100%" src="./images/github-create-repo.png" alt="GitHub 创建仓库" />

5. 你现在有了一个仓库！从浏览器复制 URL — 格式类似 `https://github.com/your-username/my-website`

---

## 2. 安装 Git、Node.js 和 Claude Code

你的电脑上需要三个工具：Git（用于管理代码）、Node.js（用于在本地运行网站）和 Claude Code（你的 AI 编程助手）。

### 安装 Git

Git 是连接你的电脑与 GitHub 的工具。

**在 Mac 上：**

1. 打开 **Terminal** 应用（在 Spotlight 中按 Cmd + Space 搜索"Terminal"）
2. 输入以下命令并按 Enter：
   ```bash
   git --version
   ```
3. 如果 Git 未安装，会弹出窗口提示你安装 Command Line Tools — 点击 **Install**
4. 等待安装完成

**在 Windows 上：**

1. 访问 [git-scm.com](https://git-scm.com)
2. 下载安装程序并运行
3. 点击 **Next** 接受所有默认选项，完成安装
4. 从开始菜单打开 **Git Bash**（用它代替普通的命令提示符）

### 配置 Git

安装后，告诉 Git 你是谁。打开 Terminal（Mac）或 Git Bash（Windows）并运行：

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

使用与 GitHub 相同的邮箱。

### 安装 Node.js

Node.js 让你在开发过程中能在电脑上运行网站。

1. 访问 [nodejs.org](https://nodejs.org)
2. 下载 **LTS** 版本（标注"Recommended for most users"的那个）
3. 运行安装程序并按默认选项操作
4. 打开 Terminal 运行以下命令来验证安装：
   ```bash
   node --version
   npm --version
   ```
   两者都应显示版本号。

### 安装 Claude Code

Claude Code 是一个在你的终端中运行并为你编写代码的 AI 助手。

1. 打开 Terminal 并运行：
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```
2. 验证安装：
   ```bash
   claude --version
   ```

---

## 3. 克隆 GitHub 仓库

"克隆"是指将你的 GitHub 仓库下载到电脑上，以便在本地进行操作。

1. 打开 Terminal
2. 导航到你想存放项目的位置。例如，将其放入"Projects"文件夹：
   ```bash
   mkdir -p ~/Projects
   cd ~/Projects
   ```
3. 克隆你的仓库（将 URL 替换为第 1 步中的实际 URL）：
   ```bash
   git clone https://github.com/your-username/my-website.git
   ```
4. 进入项目文件夹：
   ```bash
   cd my-website
   ```

你现在已进入项目文件夹，可以开始构建了。

---

## 4. 配置 Claude Code

### 购买 Claude 订阅

Claude Code 需要 Anthropic API 密钥或 Claude 订阅。

**方案 A：Anthropic API 密钥（按用量付费）**

1. 访问 [console.anthropic.com](https://console.anthropic.com)
2. 注册账户
3. 进入 **Settings** > **API Keys**
4. 点击 **Create Key** 并复制密钥
5. 在 **Settings** > **Billing** 下添加账单信息并充值（建议先充值 $10–20）

**方案 B：Claude Max 订阅（无限使用）**

1. 访问 [claude.ai](https://claude.ai)
2. 注册并订阅 **Max 计划**（每月 $100），包含 Claude Code 使用权限

### 将 Claude Code 连接到你的账户

1. 打开 Terminal 并导航到你的项目文件夹：
   ```bash
   cd ~/Projects/my-website
   ```
2. 启动 Claude Code：
   ```bash
   claude
   ```
3. 首次启动时，会提示你进行身份验证：
   - 如果使用 **API 密钥**：会提示你输入密钥
   - 如果使用 **Claude 订阅**：会打开浏览器窗口进行登录
4. 按照屏幕上的提示完成身份验证

<img width="100%" src="./images/claude-code-first-launch.png" alt="Claude Code 首次启动" />

你现在可以开始 vibe coding 了！Claude Code 会读取你的项目文件并帮助你构建网站。

---

## 5. 使用 Next.js 构建网站

Next.js 是构建现代网站的流行框架。你不需要理解它 — Claude Code 会帮你完成所有设置。

### 初始化项目

确保你在项目文件夹中，然后启动 Claude Code：

```bash
cd ~/Projects/my-website
claude
```

输入以下提示词：

```
Set up a new Next.js project in the current directory with TypeScript, Tailwind CSS,
and the App Router. Use the latest version of Next.js. Keep the default configuration
simple and clean.
```

Claude Code 将创建所有必要的文件。完成后，你可以在本地预览你的网站：

```bash
npm run dev
```

打开浏览器访问 `http://localhost:3000` 查看你的网站。

### 设计网站布局

现在告诉 Claude Code 你希望网站看起来是什么样的。以下是一些可以使用的示例提示词：

**适用于落地页：**

```
Create a modern landing page with:
- A navigation bar with the logo "MyBrand" on the left and links to
  Home, Features, Pricing, and Contact on the right
- A hero section with a big headline "Build Something Amazing",
  a subtitle, and a call-to-action button
- A features section with 3 cards showing icons, titles, and descriptions
- A footer with copyright info and social media links
Make it look professional and modern with a clean design.
```

**适用于多页网站：**

```
Create these pages for my website:
- Home page: landing page with hero, features, and testimonials
- About page: company story, team section with photos
- Pricing page: 3 pricing tiers (Basic, Pro, Enterprise) with feature comparison
- Contact page: a contact form with name, email, and message fields
Add a consistent navigation bar and footer across all pages.
```

**适用于 SaaS 产品页面：**

```
Build a SaaS landing page for a project management tool called "TaskFlow":
- Hero section with a product screenshot mockup
- Problem/solution section
- Feature showcase with 6 features in a grid
- Social proof section with customer logos
- Pricing section with monthly/yearly toggle
- FAQ section with expandable answers
- CTA section at the bottom
Use a blue and white color scheme.
```

**优化设计：**

```
Make the hero section taller, change the background to a gradient from blue to purple,
and make the headline text larger and bolder.
```

```
Add smooth scroll animations so elements fade in as the user scrolls down the page.
```

```
Make the website fully responsive so it looks great on mobile phones and tablets.
```

### Vibe Coding 技巧

- **要具体**：你给出的细节越多，结果越好
- **反复迭代**：如果效果不对，描述需要修改的地方
- **参考你喜欢的网站**：说"让它看起来像 Stripe 主页"能给 Claude Code 一个参考点
- **请求修复**：如果发现 bug，直接描述 — "导航菜单在手机上与 hero 区域重叠，请修复"

---

## 6. 配置 Stripe 支付

Stripe 让你能在网站上接受付款。你需要创建一个 Stripe 账户，然后使用 Claude Code 添加支付功能。

### 创建 Stripe 账户

1. 访问 [stripe.com](https://stripe.com)
2. 点击 **Start now** 并创建账户
3. 登录后，默认处于**测试模式**（可以在仪表板中看到切换开关）— 这非常适合开发阶段，不会收取真实费用
4. 进入 **Developers** > **API keys**
5. 你会看到两个密钥：
   - **Publishable key**：以 `pk_test_...` 开头
   - **Secret key**：以 `sk_test_...` 开头（点击显示）

6. 保持此页面打开 — 你需要这两个密钥

### 在 Stripe 中创建产品

1. 在 Stripe 仪表板中，进入 **Product catalog** > **Add product**
2. 创建你的定价套餐：
   - 名称："Basic Plan"
   - 价格：$9/月（或你想要的任何价格）
   - 点击 **Save product**
3. 重复上述步骤创建其他套餐（Pro、Enterprise 等）
4. 对于每个产品，复制 **Price ID**（以 `price_...` 开头）— 你之后会用到这些

### 将 Stripe 添加到你的网站

在项目文件夹中启动 Claude Code 并使用以下提示词：

**配置 Stripe 集成：**

```
Add Stripe payment integration to my Next.js project:
1. Install the Stripe packages (stripe and @stripe/stripe-js)
2. Create a .env.local file for my Stripe API keys with these placeholders:
   NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_xxx
   STRIPE_SECRET_KEY=sk_test_xxx
3. Create an API route at /api/checkout that creates a Stripe checkout session
4. The checkout should redirect to a /success page after payment
   and a /cancel page if they cancel
```

**添加带结账功能的定价页面：**

```
Create a pricing page with 3 tiers:
- Basic: $9/month - 5 projects, basic support
- Pro: $29/month - unlimited projects, priority support
- Enterprise: $99/month - everything in Pro plus dedicated account manager

Each tier should have a "Get Started" button that redirects to Stripe Checkout.
Use these Stripe Price IDs:
- Basic: price_xxxxx (replace with your real price ID)
- Pro: price_xxxxx
- Enterprise: price_xxxxx
```

**添加真实的 Stripe 密钥：**

```
Update the .env.local file with my real Stripe keys:
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_your_actual_key_here
STRIPE_SECRET_KEY=sk_test_your_actual_key_here
```

### 测试支付

1. 使用 `npm run dev` 在本地运行网站
2. 进入定价页面并点击购买按钮
3. 在 Stripe 结账页面，使用测试卡号：`4242 4242 4242 4242`
   - 有效期：任意未来日期
   - CVC：任意 3 位数字
4. 完成购买 — 你应该会跳转到成功页面
5. 在 Stripe 仪表板的 **Payments** 下查看测试支付记录

### 开启真实支付

当你准备好接受真实付款时：

1. 完成 Stripe 账户设置（商业信息、银行账户）
2. 在 Stripe 仪表板中从**测试模式**切换到**实时模式**
3. 复制你的实时 API 密钥（以 `pk_live_` 和 `sk_live_` 开头）
4. 用实时密钥更新你的 `.env.local`

---

## 7. 配置 DigitalOcean 服务器

你需要一台服务器来托管网站，这样任何人都能通过互联网访问它。

### 创建 DigitalOcean 账户

1. 访问 [digitalocean.com](https://www.digitalocean.com)
2. 点击 **Sign up** 并创建账户
3. 添加付款方式（信用卡或 PayPal）
4. 作为新用户，你可能会获得 60 天内 $200 的免费额度

### 创建服务器（Droplet）

1. 登录后，点击 **Create** > **Droplets**
2. 选择以下设置：
   - **Region**：选择离你的用户最近的地区（例如旧金山、纽约、伦敦）
   - **Image**：选择 **Ubuntu 22.04 (LTS)** 或最新的 Ubuntu LTS
   - **Size**：选择 **Basic** > **Regular** > **$12/mo**（2 GB 内存 / 1 CPU）— 入门足够了
   - **Authentication**：选择 **Password** 并设置一个强密码（请妥善保存！）
3. 点击 **Create Droplet**
4. 等待约 60 秒启动完成
5. 复制显示的 **IP 地址**（例如 `164.90.xxx.xxx`）— 你之后会用到

---

## 8. 安装和配置 Dokploy

Dokploy 是一个免费的开源工具，让部署网站变得像点击按钮一样简单。它类似于更简单版本的 Vercel 或 Heroku，但运行在你自己的服务器上。

### 在服务器上安装 Dokploy

1. 打开你电脑上的 Terminal
2. 通过 SSH 连接到你的服务器：
   ```bash
   ssh root@your-server-ip-address
   ```
3. 询问指纹时输入 `yes`，然后输入服务器密码
4. 连接后，运行 Dokploy 安装命令：
   ```bash
   curl -sSL https://dokploy.com/install.sh | sh
   ```
5. 等待安装完成（需要几分钟）
6. 完成后，会显示类似 `http://your-server-ip:3000` 的 URL

### 配置 Dokploy

1. 打开浏览器访问 `http://your-server-ip:3000`
2. 你会看到 Dokploy 设置界面
3. 创建管理员账户：
   - 输入你的邮箱
   - 创建密码
   - 点击 **Register**
4. 你现在进入了 Dokploy 仪表板

### 将 Dokploy 连接到 GitHub

这让 Dokploy 能自动从 GitHub 拉取你的代码。

1. 在 Dokploy 中，进入 **Settings**（齿轮图标）> **Git Providers**
2. 点击 **Add GitHub**
3. 你会被重定向到 GitHub — 点击 **Authorize** 授权 Dokploy 访问
4. 选择 Dokploy 可以访问哪些仓库：
   - 选择 **Only select repositories** 并选择你的网站仓库
   - 点击 **Install & Authorize**
5. 你会被重定向回 Dokploy — 连接现已激活

---

## 9. 部署网站

### 将代码推送到 GitHub

部署前，你需要将代码推送到 GitHub。回到本地 Terminal（不是服务器 SSH 会话）并执行：

1. 打开 Terminal 并进入你的项目文件夹：
   ```bash
   cd ~/Projects/my-website
   ```
2. 将所有文件添加到 Git：
   ```bash
   git add .
   ```
3. 创建一个提交（代码快照）：
   ```bash
   git commit -m "Initial website build"
   ```
4. 推送到 GitHub：
   ```bash
   git push origin main
   ```

如果这是你第一次推送，Git 可能会要求你登录 GitHub。按照提示操作即可。

**提示：** 你也可以通过 Claude Code 完成此操作：

```
Commit all changes with the message "Initial website build" and push to GitHub.
```

### 在 Dokploy 中创建应用

1. 在 Dokploy 仪表板中，点击侧边栏的 **Projects**

<img width="100%" src="./images/dokploy-projects.png" alt="Dokploy 项目" />

2. 点击 **Create Project** 并命名（例如"My Website"）
3. 在项目内，点击 **Create Service** > **Application**
4. 配置应用：
   - **Name**：给它起个名字（例如"web"）
   - **Source**：选择 **GitHub**
   - **Repository**：选择你的网站仓库
   - **Branch**：`main`
   - **Build Type**：选择 **Nixpacks**（自动检测你的项目类型）
5. 点击 **Save**

### 配置环境变量

你的网站需要 Stripe 密钥才能在生产环境中正常运行。

1. 在 Dokploy 的应用设置中，进入 **Environment** 标签
2. 添加你的环境变量（每行一个）：
   ```
   NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_live_your_key
   STRIPE_SECRET_KEY=sk_live_your_key
   ```
3. 点击 **Save**

### 配置域名（可选但推荐）

如果你有域名：

1. 在 Dokploy 中，进入你的应用 > **Domains** 标签
2. 点击 **Add Domain**
3. 输入你的域名（例如 `www.mywebsite.com`）
4. 启用 **HTTPS**（通过 Let's Encrypt 提供免费 SSL 证书）
5. 点击 **Save**
6. 在你的域名注册商处（购买域名的地方），添加 DNS 记录：
   - **Type**：A
   - **Name**：`@`（或 `www`）
   - **Value**：你服务器的 IP 地址
   - **TTL**：3600

### 部署

1. 在 Dokploy 中，进入你的应用并点击 **Deploy**
2. 查看构建日志 — Dokploy 将：
   - 从 GitHub 拉取你的代码
   - 安装依赖
   - 构建你的 Next.js 网站
   - 启动运行
3. 构建完成后，你的网站就上线了！

### 推送后自动部署

Dokploy 可以在你每次向 GitHub 推送新代码时自动部署：

1. 在应用设置中，进入 **General** 标签
2. 启用 **Auto Deploy**
3. 现在，每次你向 GitHub 推送代码，Dokploy 都会自动重新构建并部署

### 完整工作流程：修改并部署

以下是你日常更新网站的工作流程：

1. 打开 Terminal，导航到你的项目，启动 Claude Code：
   ```bash
   cd ~/Projects/my-website
   claude
   ```
2. 告诉 Claude Code 要做什么修改：
   ```
   Change the hero headline to "Welcome to the Future" and update the
   background color to dark blue.
   ```
3. 在 `http://localhost:3000` 本地预览（运行 `npm run dev`）
4. 满意后，提交并推送：
   ```bash
   git add .
   git commit -m "Update hero section"
   git push origin main
   ```
5. Dokploy 自动部署你的修改。完成！

---

## 10. 配置 Google Analytics

Google Analytics 让你能查看有多少人访问你的网站、他们来自哪里，以及他们浏览了哪些页面。

### 创建 Google Analytics 账户

1. 访问 [analytics.google.com](https://analytics.google.com)
2. 点击 **Start measuring**
3. 填写账户详情：
   - **Account name**：你的姓名或企业名称
   - 点击 **Next**
4. 创建媒体资源：
   - **Property name**：你的网站名称
   - 选择你的时区和货币
   - 点击 **Next**
5. 填写你的业务详情并点击 **Create**
6. 接受服务条款

### 获取你的衡量 ID

1. 在 Google Analytics 中，进入 **Admin**（齿轮图标）> **Data Streams**
2. 点击 **Add stream** > **Web**
3. 输入你的网站 URL 和数据流名称
4. 点击 **Create stream**
5. 复制 **Measurement ID** — 格式类似 `G-XXXXXXXXXX`

<img width="100%" src="./images/google-analytics-measurement-id.png" alt="Google Analytics 衡量 ID" />

### 将 Google Analytics 添加到你的网站

在项目文件夹中启动 Claude Code 并使用此提示词：

```
Add Google Analytics to my Next.js project.
My Google Analytics Measurement ID is G-XXXXXXXXXX (replace with your real ID).
Set it up using the recommended approach with the Next.js Script component.
Add it to the root layout so it tracks all pages. Use an environment variable
called NEXT_PUBLIC_GA_MEASUREMENT_ID for the ID.
```

然后添加环境变量：

1. **本地**：添加到你的 `.env.local` 文件：
   ```
   NEXT_PUBLIC_GA_MEASUREMENT_ID=G-XXXXXXXXXX
   ```
2. **在 Dokploy 上**：在应用的 **Environment** 标签中添加相同的变量

### 验证是否正常工作

1. 将你的修改推送到 GitHub：
   ```bash
   git add .
   git commit -m "Add Google Analytics"
   git push origin main
   ```
2. 等待 Dokploy 部署完成
3. 访问你的线上网站
4. 进入 Google Analytics > **Reports** > **Realtime**
5. 你应该能看到自己作为活跃用户

---

## 快速参考：常用命令

| 你想做什么               | 命令                                            |
| ------------------------ | ----------------------------------------------- |
| 打开 Terminal            | Cmd + Space，输入"Terminal"（Mac）              |
| 进入项目文件夹           | `cd ~/Projects/my-website`                      |
| 启动 Claude Code         | `claude`                                        |
| 本地运行网站             | `npm run dev`                                   |
| 停止本地服务器           | 在 Terminal 中按 `Ctrl + C`                     |
| 将修改保存到 Git         | `git add .` 然后 `git commit -m "your message"` |
| 推送到 GitHub            | `git push origin main`                          |
| 拉取最新代码             | `git pull origin main`                          |
| 查看项目状态             | `git status`                                    |
| 连接到你的服务器         | `ssh root@your-server-ip`                       |

## 故障排除

**"command not found: node"**
Node.js 未正确安装。从 [nodejs.org](https://nodejs.org) 重新安装。

**"command not found: claude"**
重新运行 `npm install -g @anthropic-ai/claude-code`。

**Git 每次都要求输入用户名/密码**
设置 SSH 密钥或使用 GitHub CLI（`gh auth login`）。

**网站在本地正常但部署后不工作**
检查 Dokploy 的 Environment 标签中是否已设置环境变量。

**Stripe 支付在生产环境中不工作**
确保你使用的是实时密钥（不是测试密钥），并且已在 Dokploy 的环境变量中设置。

**Dokploy 构建失败**
在 Dokploy 中查看构建日志中的错误信息。复制错误并粘贴给 Claude Code：

```
I'm getting this error when deploying: [paste error here]. How do I fix it?
```

---

## 总结

以下是你所完成的事情：

1. **GitHub** — 你的代码已存储并进行版本控制
2. **Git + Node.js + Claude Code** — 你的本地开发工具包
3. **Next.js** — 现代、快速的网站框架
4. **Stripe** — 接受客户付款
5. **DigitalOcean + Dokploy** — 你的网站已在互联网上线
6. **Google Analytics** — 你可以追踪访客并衡量增长

这套配置的美妙之处在于它未来的工作流程：打开 Claude Code，描述你想要的修改，提交，推送，即刻上线。享受 vibe coding 的乐趣！
