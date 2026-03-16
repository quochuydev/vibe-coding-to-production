# Vibe Coding to Production

🇺🇸 [English](README.md) | 🇨🇳 [中文](README-zh.md) | 🇻🇳 [Tiếng Việt](README-vi.md) | 🇪🇸 [Español](README-es.md) | 🇩🇪 [Deutsch](README-de.md)

A complete step-by-step guide for **non-developers** to build a website from scratch and deploy it to production using AI-assisted coding (vibe coding) with Claude Code.

By the end of this guide, you will have:

- A fully functional Next.js website
- Stripe payment integration
- Deployed to a live server with Dokploy
- Google Analytics tracking set up

No prior coding experience required. Let's go.

---

## Table of Contents

1. [Create a GitHub Account & Repository](#1-create-a-github-account--repository)
2. [Install Git, Node.js & Claude Code](#2-install-git-nodejs--claude-code)
3. [Clone Your GitHub Repository](#3-clone-your-github-repository)
4. [Set Up Claude Code](#4-set-up-claude-code)
5. [Build Your Website with Next.js](#5-build-your-website-with-nextjs)
6. [Set Up Stripe Payments](#6-set-up-stripe-payments)
7. [Set Up a DigitalOcean Server](#7-set-up-a-digitalocean-server)
8. [Install & Configure Dokploy](#8-install--configure-dokploy)
9. [Deploy Your Website](#9-deploy-your-website)
10. [Set Up Google Analytics](#10-set-up-google-analytics)

---

## 1. Create a GitHub Account & Repository

GitHub is where your website code will live. Think of it as a cloud folder for your project that also tracks every change you make.

### Create a GitHub Account

1. Go to [github.com](https://github.com)
2. Click **Sign up**
3. Enter your email, create a password, and choose a username
4. Complete the verification and click **Create account**
5. Check your email and verify your account

### Create a New Repository

A repository (or "repo") is like a project folder on GitHub.

1. After logging in, click the **+** icon in the top-right corner
2. Click **New repository**
3. Fill in the details:
   - **Repository name**: choose a name for your project (e.g., `my-website`)
   - **Description**: optional, add a short description
   - **Public** or **Private**: choose Private if you don't want others to see your code
   - Check **Add a README file**
4. Click **Create repository**

<img width="100%" src="./images/github-create-repo.png" alt="GitHub Create Repository" />

5. You now have a repository! Copy the URL from your browser — it looks like `https://github.com/your-username/my-website`

---

## 2. Install Git, Node.js & Claude Code

You need three tools on your computer: Git (to manage code), Node.js (to run your website locally), and Claude Code (your AI coding assistant).

### Install Git

Git is the tool that connects your computer to GitHub.

**On Mac:**

1. Open the **Terminal** app (search "Terminal" in Spotlight with Cmd + Space)
2. Type the following and press Enter:
   ```bash
   git --version
   ```
3. If Git is not installed, a popup will ask you to install Command Line Tools — click **Install**
4. Wait for the installation to finish

**On Windows:**

1. Go to [git-scm.com](https://git-scm.com)
2. Download the installer and run it
3. Click **Next** through all the default options and finish the installation
4. Open **Git Bash** from your Start menu (use this instead of the regular command prompt)

### Configure Git

After installing, tell Git who you are. Open your Terminal (Mac) or Git Bash (Windows) and run:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

Use the same email you used for GitHub.

### Install Node.js

Node.js lets you run your website on your computer during development.

1. Go to [nodejs.org](https://nodejs.org)
2. Download the **LTS** version (the one that says "Recommended for most users")
3. Run the installer and follow the default options
4. Verify it's installed by opening Terminal and running:
   ```bash
   node --version
   npm --version
   ```
   Both should show a version number.

### Install Claude Code

Claude Code is an AI assistant that runs in your terminal and writes code for you.

1. Open Terminal and run:
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```
2. Verify it's installed:
   ```bash
   claude --version
   ```

---

## 3. Clone Your GitHub Repository

"Cloning" means downloading your GitHub repo to your computer so you can work on it locally.

1. Open Terminal
2. Navigate to where you want your project to live. For example, to put it in a "Projects" folder:
   ```bash
   mkdir -p ~/Projects
   cd ~/Projects
   ```
3. Clone your repo (replace with your actual URL from Step 1):
   ```bash
   git clone https://github.com/your-username/my-website.git
   ```
4. Go into the project folder:
   ```bash
   cd my-website
   ```

You're now inside your project folder and ready to start building.

---

## 4. Set Up Claude Code

### Buy a Claude Subscription

Claude Code requires an Anthropic API key or a Claude subscription.

**Option A: Anthropic API Key (Pay as you go)**

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Sign up for an account
3. Go to **Settings** > **API Keys**
4. Click **Create Key** and copy it
5. Add billing info under **Settings** > **Billing** and add credits (start with $10–20)

**Option B: Claude Max Subscription (Unlimited usage)**

1. Go to [claude.ai](https://claude.ai)
2. Sign up and subscribe to the **Max plan** ($100/month) which includes Claude Code usage

### Connect Claude Code to Your Account

1. Open Terminal and navigate to your project folder:
   ```bash
   cd ~/Projects/my-website
   ```
2. Start Claude Code:
   ```bash
   claude
   ```
3. On first launch, it will ask you to authenticate:
   - If using an **API Key**: it will prompt you to enter your key
   - If using a **Claude subscription**: it will open a browser window to log in
4. Follow the on-screen instructions to complete authentication

<img width="100%" src="./images/claude-code-first-launch.png" alt="Claude Code First Launch" />

You're now ready to vibe code! Claude Code will read your project files and help you build your website.

---

## 5. Build Your Website with Next.js

Next.js is a popular framework for building modern websites. You don't need to understand it — Claude Code will set everything up for you.

### Initialize the Project

Make sure you are in your project folder, then start Claude Code:

```bash
cd ~/Projects/my-website
claude
```

Type the following prompt:

```
Set up a new Next.js project in the current directory with TypeScript, Tailwind CSS,
and the App Router. Use the latest version of Next.js. Keep the default configuration
simple and clean.
```

Claude Code will create all the necessary files. When it's done, you can preview your site locally:

```bash
npm run dev
```

Open your browser and go to `http://localhost:3000` to see your website.

<img width="100%" src="./images/nextjs-local-preview.png" alt="Next.js Local Preview" />

### Design Your Website Layout

Now tell Claude Code what you want your website to look like. Here are some sample prompts you can use:

**For a landing page:**

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

**For a multi-page website:**

```
Create these pages for my website:
- Home page: landing page with hero, features, and testimonials
- About page: company story, team section with photos
- Pricing page: 3 pricing tiers (Basic, Pro, Enterprise) with feature comparison
- Contact page: a contact form with name, email, and message fields
Add a consistent navigation bar and footer across all pages.
```

**For a SaaS product page:**

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

**To refine the design:**

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

### Tips for Vibe Coding

- **Be specific**: the more detail you give, the better the result
- **Iterate**: if something doesn't look right, describe what to change
- **Reference sites you like**: "Make it look like the Stripe homepage" gives Claude Code a reference point
- **Ask for fixes**: if you see a bug, just describe it — "The navigation menu is overlapping the hero section on mobile, please fix it"

---

## 6. Set Up Stripe Payments

Stripe lets you accept payments on your website. You'll set up a Stripe account and then use Claude Code to add payment functionality.

### Create a Stripe Account

1. Go to [stripe.com](https://stripe.com)
2. Click **Start now** and create an account
3. After logging in, you'll be in **Test mode** by default (you can see a toggle in the dashboard) — this is perfect for building; no real money is charged
4. Go to **Developers** > **API keys**
5. You'll see two keys:
   - **Publishable key**: starts with `pk_test_...`
   - **Secret key**: starts with `sk_test_...` (click to reveal)

<img width="100%" src="./images/stripe-api-keys.png" alt="Stripe API Keys" />

6. Keep this page open — you'll need both keys

### Create Products in Stripe

1. In the Stripe Dashboard, go to **Product catalog** > **Add product**
2. Create your pricing tiers:
   - Name: "Basic Plan"
   - Price: $9/month (or whatever you want)
   - Click **Save product**
3. Repeat for other tiers (Pro, Enterprise, etc.)
4. For each product, copy the **Price ID** (starts with `price_...`) — you'll need these

### Add Stripe to Your Website

Start Claude Code in your project folder and use these prompts:

**Set up Stripe integration:**

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

**Add a pricing page with checkout:**

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

**Add your real Stripe keys:**

```
Update the .env.local file with my real Stripe keys:
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_your_actual_key_here
STRIPE_SECRET_KEY=sk_test_your_actual_key_here
```

### Test Payments

1. Run your website locally with `npm run dev`
2. Go to the pricing page and click a purchase button
3. On the Stripe checkout page, use the test card number: `4242 4242 4242 4242`
   - Expiry: any future date
   - CVC: any 3 digits
4. Complete the purchase — you should be redirected to the success page
5. Check your Stripe Dashboard under **Payments** to see the test payment

<img width="100%" src="./images/stripe-test-payment.png" alt="Stripe Test Payment" />

### Go Live with Real Payments

When you're ready for real payments:

1. Complete your Stripe account setup (business details, bank account)
2. Toggle from **Test mode** to **Live mode** in the Stripe Dashboard
3. Copy your live API keys (they start with `pk_live_` and `sk_live_`)
4. Update your `.env.local` with the live keys

---

## 7. Set Up a DigitalOcean Server

You need a server to host your website so anyone can access it on the internet.

### Create a DigitalOcean Account

1. Go to [digitalocean.com](https://www.digitalocean.com)
2. Click **Sign up** and create an account
3. Add a payment method (credit card or PayPal)
4. You may receive $200 in free credits for 60 days as a new user

### Create a Server (Droplet)

1. After logging in, click **Create** > **Droplets**
2. Choose the following settings:
   - **Region**: choose the closest to your users (e.g., San Francisco, New York, London)
   - **Image**: select **Ubuntu 22.04 (LTS)** or the latest Ubuntu LTS
   - **Size**: select **Basic** > **Regular** > **$12/mo** (2 GB RAM / 1 CPU) — this is enough to start
   - **Authentication**: choose **Password** and set a strong root password (save this somewhere safe!)
3. Click **Create Droplet**
4. Wait about 60 seconds for it to spin up
5. Copy the **IP address** shown (e.g., `164.90.xxx.xxx`) — you'll need this

<img width="100%" src="./images/digitalocean-create-droplet.png" alt="DigitalOcean Create Droplet" />

---

## 8. Install & Configure Dokploy

Dokploy is a free, open-source tool that makes deploying your website as easy as clicking a button. It's like a simpler version of Vercel or Heroku that runs on your own server.

### Install Dokploy on Your Server

1. Open Terminal on your computer
2. Connect to your server via SSH:
   ```bash
   ssh root@your-server-ip-address
   ```
3. Type `yes` when asked about the fingerprint, then enter your server password
4. Once connected, run the Dokploy installation command:
   ```bash
   curl -sSL https://dokploy.com/install.sh | sh
   ```
5. Wait for the installation to complete (this takes a few minutes)
6. When done, it will show a URL like `http://your-server-ip:3000`

### Set Up Dokploy

1. Open your browser and go to `http://your-server-ip:3000`
2. You'll see the Dokploy setup screen
3. Create an admin account:
   - Enter your email
   - Create a password
   - Click **Register**
4. You're now in the Dokploy dashboard

<img width="100%" src="./images/dokploy-setup-screen.png" alt="Dokploy Setup Screen" />

### Connect Dokploy to GitHub

This lets Dokploy pull your code from GitHub automatically.

1. In Dokploy, go to **Settings** (gear icon) > **Git Providers**
2. Click **Add GitHub**
3. You'll be redirected to GitHub — click **Authorize** to give Dokploy access
4. Select which repositories Dokploy can access:
   - Choose **Only select repositories** and pick your website repo
   - Click **Install & Authorize**
5. You'll be redirected back to Dokploy — the connection is now active

<img width="100%" src="./images/dokploy-github-connection.png" alt="Dokploy GitHub Connection" />

---

## 9. Deploy Your Website

### Push Your Code to GitHub

Before deploying, you need to push your code to GitHub. Go back to your local Terminal (not the server SSH session) and do:

1. Open Terminal and go to your project folder:
   ```bash
   cd ~/Projects/my-website
   ```
2. Add all your files to Git:
   ```bash
   git add .
   ```
3. Create a commit (a snapshot of your code):
   ```bash
   git commit -m "Initial website build"
   ```
4. Push it to GitHub:
   ```bash
   git push origin main
   ```

If this is your first push, Git may ask you to log in to GitHub. Follow the prompts.

**Tip:** You can also do this through Claude Code:

```
Commit all changes with the message "Initial website build" and push to GitHub.
```

### Create an Application in Dokploy

1. In the Dokploy dashboard, click **Projects** in the sidebar

<img width="100%" src="./images/dokploy-projects.png" alt="Dokploy Projects" />

2. Click **Create Project** and give it a name (e.g., "My Website")
3. Inside the project, click **Create Service** > **Application**
4. Configure the application:
   - **Name**: give it a name (e.g., "web")
   - **Source**: select **GitHub**
   - **Repository**: select your website repository
   - **Branch**: `main`
   - **Build Type**: select **Nixpacks** (auto-detects your project type)
5. Click **Save**

### Set Up Environment Variables

Your website needs the Stripe keys to work in production.

1. In your application settings in Dokploy, go to the **Environment** tab
2. Add your environment variables (one per line):
   ```
   NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_live_your_key
   STRIPE_SECRET_KEY=sk_live_your_key
   ```
3. Click **Save**

### Set Up a Domain (Optional but Recommended)

If you have a domain name:

1. In Dokploy, go to your application > **Domains** tab
2. Click **Add Domain**
3. Enter your domain (e.g., `www.mywebsite.com`)
4. Enable **HTTPS** (free SSL certificate via Let's Encrypt)
5. Click **Save**
6. In your domain registrar (where you bought the domain), add a DNS record:
   - **Type**: A
   - **Name**: `@` (or `www`)
   - **Value**: your server's IP address
   - **TTL**: 3600

### Deploy

1. In Dokploy, go to your application and click **Deploy**
2. Watch the build logs — Dokploy will:
   - Pull your code from GitHub
   - Install dependencies
   - Build your Next.js website
   - Start it up
3. Once the build is complete, your website is live!

<img width="100%" src="./images/dokploy-deploy-logs.png" alt="Dokploy Deploy Logs" />

### Auto-Deploy on Push

Dokploy can auto-deploy every time you push new code to GitHub:

1. In your application settings, go to the **General** tab
2. Enable **Auto Deploy**
3. Now, whenever you push code to GitHub, Dokploy automatically rebuilds and deploys

### The Full Workflow: Make Changes and Deploy

Here's your day-to-day workflow for updating your website:

1. Open Terminal, navigate to your project, and start Claude Code:
   ```bash
   cd ~/Projects/my-website
   claude
   ```
2. Tell Claude Code what to change:
   ```
   Change the hero headline to "Welcome to the Future" and update the
   background color to dark blue.
   ```
3. Preview locally at `http://localhost:3000` (run `npm run dev`)
4. When happy with the changes, commit and push:
   ```bash
   git add .
   git commit -m "Update hero section"
   git push origin main
   ```
5. Dokploy auto-deploys your changes. Done!

---

## 10. Set Up Google Analytics

Google Analytics lets you see how many people visit your website, where they come from, and what pages they view.

### Create a Google Analytics Account

1. Go to [analytics.google.com](https://analytics.google.com)
2. Click **Start measuring**
3. Fill in the account details:
   - **Account name**: your name or business name
   - Click **Next**
4. Create a property:
   - **Property name**: your website name
   - Select your timezone and currency
   - Click **Next**
5. Fill in your business details and click **Create**
6. Accept the terms of service

### Get Your Measurement ID

1. In Google Analytics, go to **Admin** (gear icon) > **Data Streams**
2. Click **Add stream** > **Web**
3. Enter your website URL and a stream name
4. Click **Create stream**
5. Copy the **Measurement ID** — it looks like `G-XXXXXXXXXX`

<img width="100%" src="./images/google-analytics-measurement-id.png" alt="Google Analytics Measurement ID" />

### Add Google Analytics to Your Website

Start Claude Code in your project folder and use this prompt:

```
Add Google Analytics to my Next.js project.
My Google Analytics Measurement ID is G-XXXXXXXXXX (replace with your real ID).
Set it up using the recommended approach with the Next.js Script component.
Add it to the root layout so it tracks all pages. Use an environment variable
called NEXT_PUBLIC_GA_MEASUREMENT_ID for the ID.
```

Then add the environment variable:

1. **Locally**: add to your `.env.local` file:
   ```
   NEXT_PUBLIC_GA_MEASUREMENT_ID=G-XXXXXXXXXX
   ```
2. **On Dokploy**: add the same variable in your application's **Environment** tab

### Verify It's Working

1. Push your changes to GitHub:
   ```bash
   git add .
   git commit -m "Add Google Analytics"
   git push origin main
   ```
2. Wait for Dokploy to deploy
3. Visit your live website
4. Go to Google Analytics > **Reports** > **Realtime**
5. You should see yourself as an active user

---

## Quick Reference: Useful Commands

| What you want to do       | Command                                         |
| ------------------------- | ----------------------------------------------- |
| Open Terminal             | Cmd + Space, type "Terminal" (Mac)              |
| Go to your project folder | `cd ~/Projects/my-website`                      |
| Start Claude Code         | `claude`                                        |
| Run your website locally  | `npm run dev`                                   |
| Stop the local server     | Press `Ctrl + C` in Terminal                    |
| Save your changes to Git  | `git add .` then `git commit -m "your message"` |
| Push to GitHub            | `git push origin main`                          |
| Pull latest code          | `git pull origin main`                          |
| Check project status      | `git status`                                    |
| Connect to your server    | `ssh root@your-server-ip`                       |

## Troubleshooting

**"command not found: node"**
Node.js isn't installed properly. Reinstall from [nodejs.org](https://nodejs.org).

**"command not found: claude"**
Run `npm install -g @anthropic-ai/claude-code` again.

**Git asks for username/password every time**
Set up SSH keys or use the GitHub CLI (`gh auth login`).

**Website works locally but not after deploy**
Check that your environment variables are set in Dokploy's Environment tab.

**Stripe payments not working in production**
Make sure you're using live keys (not test keys) and they are set in Dokploy's environment variables.

**Build fails on Dokploy**
Check the build logs in Dokploy for error messages. Copy the error and paste it to Claude Code:

```
I'm getting this error when deploying: [paste error here]. How do I fix it?
```

---

## Summary

Here's what you've accomplished:

1. **GitHub** — your code is stored and version-controlled
2. **Git + Node.js + Claude Code** — your local development toolkit
3. **Next.js** — a modern, fast website framework
4. **Stripe** — accept payments from customers
5. **DigitalOcean + Dokploy** — your website is live on the internet
6. **Google Analytics** — you can track visitors and measure growth

The beauty of this setup is the workflow going forward: open Claude Code, describe what you want to change, commit, push, and it's live. Happy vibe coding!
