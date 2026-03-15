# Jared Burck's Personal Site - AI Guidelines

Context: This is the source code for Jared Burck's personal portfolio and blog. Jared is a Managing Architect at Red Hat with a focus on OpenShift, AI, Automation, and Open Source. The site should reflect professional architectural standards and clean, modern web practices.

## 🛠 Tech Stack & Environment
- **Primary Framework:** Hugo, CareerCanvas Theme (by Felipe Cordero)
- **Hosting:** Cloudflare Pages
- **Environment:** macOS (Homebrew), Node.js/npm (for assets/scripts)
- **Deployment:** Automatic via Cloudflare Pages and GitHub Actions as alternative (but not used today for deployment)

## 📜 Coding Standards
- **General:** Prefer semantic HTML5 and accessible (A11Y) components
- **Styling:** Follow the existing theme's CSS/SCSS patterns. If using Tailwind, avoid over-nesting classes
- **Content:** Blog posts are in Markdown (`content/posts/`). Front-matter should use YAML
- **Naming:** Use kebab-case for filenames and image assets
- **Tone:** Professional, technical, and architecturally focused (consistent with a Red Hat Managing Architect profile)

## 🚀 Key Commands
- **Development:** `hugo server -D`
- **Build:** `hugo --gc --minify` OR `npm run build`
- **Linting:** `npm run lint` (if configured)
- **New Content:** `hugo new posts/my-new-post.md`

## 🏗 Architecture Decisions
- **Structure:** - `/content`: All Markdown and media assets.
  - `/layouts` or `/src/components`: Custom overrides and UI components.
  - `/static` or `/public`: Global assets like favicons or PDFs.
- **Data-Driven:** Prefer using data files (`data/` or `src/data/`) for resume items (skills, experience) rather than hardcoding in HTML.
- **Architecture over Hacks:** When adding features, prioritize sustainable, theme-compliant methods over quick CSS hacks.

## ✅ Verification Checklist
- Before finished: 
  - Run the local build command to ensure no breakage.
  - Check that Markdown front-matter follows the project's required schema (e.g., date, categories, author).
  - IMPORTANT: If adding images, ensure they are optimized for web performance.
