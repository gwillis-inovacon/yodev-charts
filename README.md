# yoDEV Charts - Data Visualization Hub

A dedicated site for hosting interactive financial and data visualizations for the yoDEV community.

## 🚀 Quick Start

### Prerequisites
- Git installed
- GitHub account
- Netlify account (free)

### Setup Instructions

1. **Initialize the project locally:**
   ```bash
   mkdir yodev-charts
   cd yodev-charts
   # Copy all project files into this directory
   ```

2. **Initialize Git and push to GitHub:**
   ```bash
   git init
   git add .
   git commit -m "Initial commit: yoDEV Charts project"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/yodev-charts.git
   git push -u origin main
   ```

3. **Deploy to Netlify:**
   - Go to [Netlify](https://app.netlify.com)
   - Click "Add new site" → "Import an existing project"
   - Connect your GitHub account
   - Select the `yodev-charts` repository
   - Deploy! (Netlify will auto-detect settings from netlify.toml)

4. **Configure custom domain (optional):**
   - In Netlify: Site settings → Domain management
   - Add custom domain: `charts.yodev.dev` or similar
   - Update DNS records as instructed

## 📊 Adding New Charts

### Method 1: Using Claude
1. Ask Claude to create a new chart
2. Request it as a standalone HTML file with OpenGraph tags
3. Save in the `charts/` directory
4. Update `index.html` to add the new chart to the gallery
5. Commit and push:
   ```bash
   git add .
   git commit -m "Add new chart: [chart name]"
   git push
   ```
6. Netlify auto-deploys! ✨

### Method 2: Manual Creation
1. Create new HTML file in `charts/` directory
2. Use existing chart files as templates
3. Update OpenGraph meta tags (title, description, image)
4. Add entry to gallery in `index.html`
5. Commit and push

## 🏗️ Project Structure

```
yodev-charts/
├── index.html                          # Gallery landing page
├── charts/
│   ├── global-equity-2025.html        # Global equity returns comparison
│   ├── april-volatility-2025.html     # April 2025 crash timeline
│   └── annual-returns-2023-2025.html  # Multi-year comparison
├── netlify.toml                        # Netlify configuration
├── .gitignore                          # Git ignore file
└── README.md                           # This file
```

## 🔗 Using Charts in Discourse

Once deployed, each chart has its own URL:
- `https://your-site.netlify.app/charts/global-equity-2025.html`
- `https://your-site.netlify.app/charts/april-volatility-2025.html`
- etc.

Simply paste these URLs in your Discourse posts and they'll generate nice preview cards with thumbnails!

## 🎨 Customization

### Branding
- Update colors and styling in individual chart files
- Modify the gallery page (`index.html`) with yoDEV branding
- Add logo or header images

### OpenGraph Images
For better Discourse previews, you can:
1. Take screenshots of charts
2. Upload to `assets/images/`
3. Update OpenGraph `og:image` meta tags in each chart HTML

## 📝 Chart Template

Here's the basic structure for creating new charts:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chart Title - yoDEV Charts</title>
    
    <!-- OpenGraph Meta Tags for Discourse -->
    <meta property="og:title" content="Chart Title">
    <meta property="og:description" content="Chart description">
    <meta property="og:type" content="website">
    <meta property="og:image" content="URL_TO_PREVIEW_IMAGE">
    
    <!-- React & Recharts from CDN -->
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/recharts@2.5.0/dist/Recharts.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
    <div id="root"></div>
    <script>
        // Your chart code here
    </script>
</body>
</html>
```

## 🔄 Continuous Deployment

Every push to the `main` branch automatically triggers a deployment on Netlify. No manual intervention needed!

## 🆘 Troubleshooting

**Deployment fails:**
- Check netlify.toml configuration
- Ensure all file paths are correct
- Check Netlify build logs

**Discourse preview not working:**
- Verify OpenGraph meta tags are present
- Ensure og:image URL is absolute (not relative)
- Test with [OpenGraph Debugger](https://www.opengraph.xyz/)

**Chart not displaying:**
- Check browser console for errors
- Verify CDN resources are loading
- Test in different browsers

## 📧 Support

Questions? Reach out on the yoDEV Discourse community!

---

**Built with ❤️ for the yoDEV community**