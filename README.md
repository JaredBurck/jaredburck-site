# Jared Burck - Personal Resume Website

Personal resume website built with [Hugo](https://gohugo.io/) and the [CareerCanvas](https://github.com/felipecordero/careercanvas) theme.

## 🚀 Quick Start

### Prerequisites

- [Hugo Extended](https://gohugo.io/installation/) (v0.147.1 or higher)
- Git

### Local Development

1. Clone the repository:
   ```bash
   git clone https://github.com/jaredburck/jaredburck-site.git
   cd jaredburck-site
   ```

2. Initialize and update submodules:
   ```bash
   git submodule init
   git submodule update
   ```

3. Start the development server:
   ```bash
   hugo server
   ```

   Or use npm:
   ```bash
   npm run dev
   ```

4. Open your browser to `http://localhost:1313`

### Building for Production

```bash
hugo --minify
```

Or use npm:
```bash
npm run build
```

The generated site will be in the `public/` directory.

## 📁 Project Structure

```
jaredburck-site/
├── content/          # Site content (markdown files)
│   └── en/          # English content
├── themes/          # Hugo themes
│   └── careercanvas/ # CareerCanvas theme (git submodule)
├── static/          # Static files (images, PDFs, etc.)
├── hugo.toml        # Hugo configuration
└── README.md        # This file
```

## 🎨 Customization

Edit `hugo.toml` to customize:
- Personal information (name, email, social links)
- Site URL and base configuration
- Color palettes
- Theme settings

Edit content files in `content/en/` to update:
- About section (`about.md`)
- Skills (`skills.md`)
- Experience (`experience.md`)
- Technical projects (`technical.md`)
- Testimonials (`testimonials.md`)

## 🌐 Deployment

This site is deployed on [Cloudflare Pages](https://pages.cloudflare.com/).

### Cloudflare Pages Configuration

- **Build command**: `hugo --minify`
- **Build output directory**: `public`
- **Hugo version**: `0.155.3` (or latest extended version)

### Manual Deployment

1. Build the site: `hugo --minify`
2. Deploy the `public/` directory to Cloudflare Pages

## 📝 License

MIT License

## 🙏 Credits

- [Hugo](https://gohugo.io/) - Static site generator
- [CareerCanvas Theme](https://github.com/felipecordero/careercanvas) by Felipe Cordero
