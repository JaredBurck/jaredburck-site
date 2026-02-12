# Deployment Guide - Cloudflare Pages

This guide walks you through deploying your Hugo site to Cloudflare Pages.

## Prerequisites

1. GitHub account with repository: `jaredburck/jaredburck-site`
2. Cloudflare account (free tier works)
3. Git installed locally

## Step 1: Push to GitHub

### Initial Setup

1. **Create the GitHub repository** (if not already created):
   - Go to https://github.com/new
   - Repository name: `jaredburck-site`
   - Set it to Public or Private (your choice)
   - **Do NOT** initialize with README, .gitignore, or license (we already have these)

2. **Add GitHub remote and push**:
   ```bash
   cd jaredburck-site
   git remote add origin https://github.com/jaredburck/jaredburck-site.git
   git branch -M main
   git add .
   git commit -m "Initial commit: Hugo site with CareerCanvas theme"
   git push -u origin main
   ```

## Step 2: Configure Cloudflare Pages

### Option A: Using Cloudflare Dashboard (Recommended)

1. **Log in to Cloudflare Dashboard**:
   - Go to https://dash.cloudflare.com/
   - Navigate to **Workers & Pages** → **Pages**

2. **Create a new project**:
   - Click **Create a project**
   - Select **Connect to Git**
   - Authorize Cloudflare to access your GitHub account
   - Select repository: `jaredburck/jaredburck-site`
   - Click **Begin setup**

3. **Configure build settings**:
   - **Project name**: `jaredburck-site`
   - **Production branch**: `main`
   - **Framework preset**: `Hugo`
   - **Build command**: `hugo --minify`
   - **Build output directory**: `public`
   - **Root directory**: `/` (leave empty)
   - **Environment variables**: (optional, add if needed)
     - `HUGO_VERSION`: `0.155.3` (or latest extended version)

4. **Advanced Settings**:
   - Click **Save and Deploy**

### Option B: Using Cloudflare Wrangler CLI

1. **Install Wrangler**:
   ```bash
   npm install -g wrangler
   ```

2. **Login to Cloudflare**:
   ```bash
   wrangler login
   ```

3. **Create pages project**:
   ```bash
   wrangler pages project create jaredburck-site
   ```

4. **Deploy**:
   ```bash
   hugo --minify
   wrangler pages deploy public --project-name=jaredburck-site
   ```

## Step 3: Configure Custom Domain (Optional)

1. In Cloudflare Pages dashboard, go to your project
2. Click **Custom domains**
3. Add your domain (e.g., `jaredburck.com`)
4. Follow DNS configuration instructions
5. Update `baseURL` in `hugo.toml` to match your domain

## Step 4: Update Hugo Configuration

After deployment, update `hugo.toml` with your actual Cloudflare Pages URL:

```toml
baseURL = "https://jaredburck.pages.dev"
```

Or if using a custom domain:
```toml
baseURL = "https://jaredburck.com"
```

## Step 5: Enable Automatic Deployments

Cloudflare Pages automatically deploys on every push to the `main` branch. No additional configuration needed!

## Validation Checklist

After deployment, verify:

- [ ] Site is accessible at Cloudflare Pages URL
- [ ] All pages load correctly (Home, About, Skills, Experience)
- [ ] Images and assets load properly
- [ ] Dark mode toggle works
- [ ] Navigation menu functions correctly
- [ ] Contact form works (if configured)
- [ ] Resume PDF downloads work (if added)
- [ ] Mobile responsive design works
- [ ] Site builds successfully on each git push

## Troubleshooting

### Build Fails

1. **Check Hugo version**: Ensure Cloudflare uses Hugo Extended version
   - Add environment variable: `HUGO_VERSION=0.155.3`

2. **Check submodules**: Ensure theme submodule is initialized
   ```bash
   git submodule init
   git submodule update
   ```

3. **Check build logs**: Review Cloudflare Pages build logs for errors

### Theme Not Loading

1. Verify submodule is properly initialized:
   ```bash
   git submodule status
   ```

2. Ensure `.gitmodules` file exists and is committed

3. In Cloudflare Pages settings, ensure submodules are fetched:
   - Build command: `git submodule update --init --recursive && hugo --minify`

### Assets Not Loading

1. Check `baseURL` in `hugo.toml` matches your deployment URL
2. Verify static files are in `static/` directory
3. Check file paths are relative to site root

## Continuous Deployment

Every time you push to the `main` branch:
1. Cloudflare Pages automatically triggers a build
2. Builds your Hugo site
3. Deploys to production
4. Updates your live site

## Manual Deployment

If needed, you can manually trigger a deployment:
1. Go to Cloudflare Pages dashboard
2. Select your project
3. Click **Retry deployment** on any previous deployment

## Support

- [Cloudflare Pages Docs](https://developers.cloudflare.com/pages/)
- [Hugo Documentation](https://gohugo.io/documentation/)
- [CareerCanvas Theme](https://github.com/felipecordero/careercanvas)
