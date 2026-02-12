# Quick Start Guide - Personal Resume Website

This guide walks you through the complete setup process from creation to deployment.

## ✅ What's Already Done

Your Hugo site has been created with:
- ✅ Hugo site structure initialized
- ✅ CareerCanvas theme installed as git submodule
- ✅ Configuration files set up (`hugo.toml`, `postcss.config.js`, `tailwind.config.js`)
- ✅ Initial content structure created
- ✅ Git repository initialized
- ✅ Cloudflare Pages configuration prepared
- ✅ Site validated and builds successfully

## 🚀 Next Steps

### Step 1: Customize Your Content

**Update `hugo.toml`:**
```bash
# Edit hugo.toml and update:
- name: "Jared Burck"  # Your name
- email: "your@email.com"  # Your email
- linkedin_url: "https://linkedin.com/in/jaredburck"  # Your LinkedIn
- github_url: "https://github.com/jaredburck"  # Your GitHub
- baseURL: "https://jaredburck.pages.dev"  # Will update after deployment
```

**Update content files:**
- `content/en/about.md` - Your personal information
- `content/en/skills.md` - Your skills and expertise
- `content/en/experience.md` - Your work experience
- `content/en/technical.md` - Your technical projects
- `content/en/testimonials.md` - Testimonials (optional)

**Add assets:**
- Profile image: `static/images/profile.jpg`
- Resume PDF: `static/files/resume.pdf`
- Update `profile_image` and `resume_url_en` in `hugo.toml`

### Step 2: Push to GitHub

```bash
cd jaredburck-site

# Add all files
git add .

# Commit
git commit -m "Initial commit: Hugo site with CareerCanvas theme"

# Add GitHub remote (if not already added)
git remote add origin https://github.com/jaredburck/jaredburck-site.git

# Push to GitHub
git branch -M main
git push -u origin main
```

**Important:** If the GitHub repository doesn't exist yet:
1. Go to https://github.com/new
2. Create repository: `jaredburck-site`
3. **Do NOT** initialize with README, .gitignore, or license
4. Then run the git commands above

### Step 3: Deploy to Cloudflare Pages

#### Option A: Using Cloudflare Dashboard (Recommended)

1. **Go to Cloudflare Dashboard:**
   - Visit https://dash.cloudflare.com/
   - Navigate to **Workers & Pages** → **Pages**

2. **Create Project:**
   - Click **Create a project**
   - Select **Connect to Git**
   - Authorize Cloudflare to access GitHub
   - Select repository: `jaredburck/jaredburck-site`
   - Click **Begin setup**

3. **Configure Build Settings:**
   - **Project name**: `jaredburck-site`
   - **Production branch**: `main`
   - **Framework preset**: `Hugo`
   - **Build command**: `hugo --minify`
   - **Build output directory**: `public`
   - **Root directory**: `/` (leave empty)

4. **Environment Variables** (optional but recommended):
   - Click **Environment variables**
   - Add:
     - `HUGO_VERSION`: `0.155.3`
     - `NODE_VERSION`: `18`

5. **Submodules:**
   - Ensure **Submodules** checkbox is enabled
   - Or update build command to:
     ```
     git submodule update --init --recursive && hugo --minify
     ```

6. **Deploy:**
   - Click **Save and Deploy**
   - Wait for build to complete (usually 2-3 minutes)

#### Option B: Using Wrangler CLI

```bash
# Install Wrangler
npm install -g wrangler

# Login
wrangler login

# Create project
wrangler pages project create jaredburck-site

# Build and deploy
hugo --minify
wrangler pages deploy public --project-name=jaredburck-site
```

### Step 4: Update Configuration

After deployment, update `hugo.toml` with your actual Cloudflare Pages URL:

```toml
baseURL = "https://jaredburck.pages.dev"  # Your actual URL
```

Then commit and push:
```bash
git add hugo.toml
git commit -m "Update baseURL for Cloudflare Pages"
git push
```

### Step 5: Validate Deployment

1. **Check build status:**
   - Go to Cloudflare Pages dashboard
   - Verify build succeeded (green checkmark)

2. **Visit your site:**
   - Open your Cloudflare Pages URL
   - Test all pages and features

3. **Verify:**
   - ✅ Site loads correctly
   - ✅ All sections display
   - ✅ Navigation works
   - ✅ Dark mode works
   - ✅ Mobile responsive
   - ✅ No console errors

See `VALIDATION.md` for detailed validation checklist.

## 📝 Common Customizations

### Update Colors

Edit color palettes in `hugo.toml`:
```toml
[params.color_palettes]
  [[params.color_palettes.palette]]
    name = "custom"
    main_color = "#YOUR_COLOR"
    second_color = "#YOUR_COLOR"
    third_color = "#YOUR_COLOR"
```

### Add Resume PDF

1. Place PDF in `static/files/resume.pdf`
2. Update `hugo.toml`:
   ```toml
   resume_url_en = "/files/resume.pdf"
   ```

### Add Profile Image

1. Place image in `static/images/profile.jpg`
2. Update `hugo.toml`:
   ```toml
   profile_image = "/images/profile.jpg"
   ```

### Configure Contact Form

1. Sign up at https://formspree.io/
2. Get your endpoint URL
3. Update `hugo.toml`:
   ```toml
   formspreeendpoint = "https://formspree.io/f/YOUR_ENDPOINT"
   ```

## 🔄 Continuous Deployment

Cloudflare Pages automatically deploys on every push to `main` branch:

1. Make changes locally
2. Commit: `git commit -m "Your changes"`
3. Push: `git push`
4. Cloudflare automatically builds and deploys
5. Site updates in 2-3 minutes

## 📚 Documentation

- **Full Deployment Guide**: See `DEPLOYMENT.md`
- **Validation Checklist**: See `VALIDATION.md`
- **Hugo Docs**: https://gohugo.io/documentation/
- **CareerCanvas Theme**: https://github.com/felipecordero/careercanvas
- **Cloudflare Pages**: https://developers.cloudflare.com/pages/

## 🆘 Troubleshooting

### Build Fails

**Theme not found:**
```bash
git submodule update --init --recursive
git add .gitmodules themes/careercanvas
git commit -m "Fix submodule"
git push
```

**PostCSS errors:**
- Ensure `package.json` has PostCSS dependencies
- Check Cloudflare Pages has Node.js environment

### Site Not Loading

- Check `baseURL` matches your Cloudflare Pages URL
- Verify build output directory is `public`
- Check build logs in Cloudflare dashboard

### Submodule Issues

```bash
# Reinitialize submodule
git submodule update --init --recursive

# If still issues, remove and re-add
git submodule deinit themes/careercanvas
git rm themes/careercanvas
git submodule add https://github.com/felipecordero/careercanvas.git themes/careercanvas
```

## ✨ You're All Set!

Your personal resume website is ready to deploy. Follow the steps above to:

1. Customize your content
2. Push to GitHub
3. Deploy to Cloudflare Pages
4. Validate everything works

Good luck with your new website! 🎉
