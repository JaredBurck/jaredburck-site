# Validation Guide - Site Configuration & Deployment

This guide helps you validate that your Hugo site is properly configured and successfully deployed.

## Pre-Deployment Validation

### 1. Local Build Validation

✅ **Build the site locally:**
```bash
cd jaredburck-site
npm install  # First time only
hugo --minify
```

**Expected Result:**
- Build completes without errors
- `public/` directory is created
- No error messages in the output

✅ **Test local server:**
```bash
hugo server
# Visit http://localhost:1313
```

**Check:**
- [ ] Site loads without errors
- [ ] All sections visible (Hero, About, Skills, Experience)
- [ ] Navigation menu works
- [ ] Dark mode toggle functions
- [ ] Responsive design works (test on mobile viewport)
- [ ] No console errors in browser DevTools

### 2. Configuration Validation

✅ **Check `config.toml`:**
- [ ] `baseURL` is set (update to your Cloudflare Pages URL after deployment)
- [ ] `theme = "careercanvas"` is set
- [ ] Personal information is updated (name, email, social links)
- [ ] `resume_url_en` points to your resume PDF (if you have one)

✅ **Check content files:**
- [ ] `content/en/about.md` - Personal information updated
- [ ] `content/en/skills.md` - Your skills listed
- [ ] `content/en/experience.md` - Your work experience added
- [ ] All YAML front matter properly closed with `---`

✅ **Check theme submodule:**
```bash
git submodule status
```
- [ ] Theme submodule shows commit hash (not `-` prefix)

### 3. Git Repository Validation

✅ **Check git status:**
```bash
git status
```

**Should show:**
- [ ] All content files staged/committed
- [ ] `config.toml` committed
- [ ] `.gitmodules` file exists
- [ ] `package.json` and config files committed
- [ ] `node_modules/` is NOT tracked (in .gitignore)

✅ **Verify remote:**
```bash
git remote -v
```
- [ ] Remote points to `https://github.com/jaredburck/jaredburck-site.git`

## Deployment Validation

### 1. GitHub Repository

✅ **Verify repository exists:**
- [ ] Repository `jaredburck/jaredburck-site` exists on GitHub
- [ ] Code is pushed to `main` branch
- [ ] `.gitmodules` file is in repository
- [ ] Theme submodule is properly initialized

**If submodule shows as empty on GitHub:**
```bash
git submodule update --init --recursive
git add .gitmodules themes/careercanvas
git commit -m "Initialize theme submodule"
git push
```

### 2. Cloudflare Pages Configuration

✅ **Verify build settings:**
- [ ] **Framework preset**: Hugo
- [ ] **Build command**: `hugo --minify`
- [ ] **Build output directory**: `public`
- [ ] **Root directory**: `/` (empty)
- [ ] **Node version**: 18.x or higher (if specified)

✅ **Environment variables (if needed):**
- [ ] `HUGO_VERSION`: `0.155.3` (or latest extended)
- [ ] `NODE_VERSION`: `18` (or higher)

✅ **Build settings for submodules:**
- [ ] **Submodules**: Enabled/Checked
- [ ] Or add to build command: `git submodule update --init --recursive && hugo --minify`

### 3. Cloudflare Pages Deployment

✅ **Check deployment status:**
1. Go to Cloudflare Dashboard → Workers & Pages → Your Project
2. Check **Deployments** tab

**Expected:**
- [ ] Build status: ✅ Success (green)
- [ ] Build logs show no errors
- [ ] Deployment URL is accessible

✅ **Verify build logs:**
- [ ] Hugo version detected correctly
- [ ] Theme submodule cloned successfully
- [ ] PostCSS/Tailwind processed without errors
- [ ] Site built successfully
- [ ] No npm install errors

### 4. Live Site Validation

✅ **Access your site:**
- Visit your Cloudflare Pages URL (e.g., `https://jaredburck.pages.dev`)

**Check all pages:**
- [ ] Homepage loads correctly
- [ ] About section displays
- [ ] Skills section shows your skills
- [ ] Experience timeline displays
- [ ] Navigation menu works
- [ ] Dark mode toggle works
- [ ] Mobile responsive (test on phone or browser dev tools)
- [ ] No 404 errors
- [ ] No console errors (check browser DevTools)

✅ **Performance check:**
- [ ] Page loads quickly (< 3 seconds)
- [ ] Images load properly
- [ ] CSS styles applied correctly
- [ ] JavaScript functions work (animations, modals)

✅ **SEO & Meta:**
- [ ] Page title displays correctly
- [ ] Meta description present
- [ ] Open Graph image (if configured)
- [ ] Social media links work

## Post-Deployment Checklist

### Content Updates
- [ ] Update personal information in `config.toml`
- [ ] Add your actual resume PDF to `static/files/resume.pdf`
- [ ] Update `resume_url_en` in `config.toml` to `/files/resume.pdf`
- [ ] Add profile image to `static/images/profile.jpg`
- [ ] Update `profile_image` in `config.toml`
- [ ] Customize color palettes if desired
- [ ] Update social media links with your actual profiles

### Custom Domain (Optional)
- [ ] Add custom domain in Cloudflare Pages
- [ ] Update `baseURL` in `config.toml` to match custom domain
- [ ] Commit and push changes
- [ ] Verify DNS configuration
- [ ] Test site on custom domain

### Continuous Deployment
- [ ] Make a test change
- [ ] Commit and push to `main` branch
- [ ] Verify Cloudflare Pages auto-deploys
- [ ] Confirm changes appear on live site

## Troubleshooting

### Build Fails

**Issue**: Build fails with "theme not found"
- **Solution**: Ensure submodules are initialized:
  ```bash
  git submodule update --init --recursive
  git add .gitmodules themes/careercanvas
  git commit -m "Fix submodule"
  git push
  ```
- **Cloudflare**: Enable "Submodules" in build settings

**Issue**: PostCSS errors
- **Solution**: Ensure `package.json` includes PostCSS dependencies
- **Cloudflare**: Add `NODE_VERSION` environment variable

**Issue**: Hugo version mismatch
- **Solution**: Set `HUGO_VERSION` environment variable in Cloudflare Pages

### Site Not Loading

**Issue**: 404 errors
- **Check**: `baseURL` in `config.toml` matches deployment URL
- **Check**: Build output directory is `public`

**Issue**: Styles not loading
- **Check**: PostCSS processed correctly (check build logs)
- **Check**: CSS files exist in `public/css/`

**Issue**: Images not loading
- **Check**: Images are in `static/images/` directory
- **Check**: Image paths in content are correct

### Submodule Issues

**Issue**: Theme files missing
```bash
git submodule update --init --recursive
```

**Issue**: Submodule shows as empty on GitHub
- Ensure `.gitmodules` is committed
- Ensure submodule directory is committed (as a reference)

## Quick Validation Commands

```bash
# Check site builds locally
hugo --minify

# Check git status
git status

# Check submodule
git submodule status

# Test local server
hugo server

# Verify remote
git remote -v

# Check build output
ls -la public/
```

## Success Criteria

Your site is successfully configured and deployed when:

✅ Site builds locally without errors  
✅ Site runs on localhost without errors  
✅ Code is pushed to GitHub  
✅ Cloudflare Pages build succeeds  
✅ Live site is accessible  
✅ All pages load correctly  
✅ No console errors  
✅ Responsive design works  
✅ Dark mode works  

## Next Steps

After validation:

1. **Customize content**: Update all placeholder text with your actual information
2. **Add assets**: Add profile image, resume PDF, project images
3. **Configure contact**: Set up Formspree endpoint if using contact form
4. **Add projects**: Add your technical projects to the technical section
5. **SEO**: Optimize meta tags and descriptions
6. **Analytics**: Add Google Analytics or similar (optional)
7. **Custom domain**: Set up your custom domain (optional)

## Support Resources

- [Hugo Documentation](https://gohugo.io/documentation/)
- [CareerCanvas Theme](https://github.com/felipecordero/careercanvas)
- [Cloudflare Pages Docs](https://developers.cloudflare.com/pages/)
- [Git Submodules Guide](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
