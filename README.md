# Bailey M. Barenick - CV and Portfolio

[![Publish Quarto Website](https://github.com/BaileyMBarenick/cv/actions/workflows/publish.yml/badge.svg)](https://github.com/BaileyMBarenick/cv/actions/workflows/publish.yml)

Professional CV and blog for Bailey M. Barenick, MSc Candidate in Biotechnology at Pennsylvania State University in the Chopra Maize Genetics Lab.

## Site

Visit the live site at: https://baileymbbarenick.github.io/cv/

## About This Project

This website serves as both a professional CV and a blog platform for sharing insights about biotechnology research, data analysis, and scientific computing. The site features:

- **CV Homepage**: Comprehensive curriculum vitae with a three-image header (lab logo, DNA analysis, maize), education, research experience, technical skills, leadership activities, and a collapsible relevant coursework section
- **Blog**: Technical writing on maize genetics, biotechnology methodologies, R/Python workflows, and scientific visualization
- **Automated Deployment**: Changes pushed to the main branch automatically build and deploy via GitHub Actions

### Conversion from Jekyll to Quarto

This site was originally built with Jekyll but was converted to [Quarto](https://quarto.org) for several advantages:

- **Scientific Publishing**: Native support for R, Python, Julia, and Observable JS code execution
- **Better Formatting**: Built-in support for citations, equations, cross-references, and technical diagrams
- **Modern Themes**: Professional, responsive design optimized for academic and technical content
- **Unified Workflow**: Same tool for websites, blogs, books, presentations, and papers
- **Computational Content**: Ability to embed live code, data visualizations, and interactive elements

## Technology Stack

- **Framework**: [Quarto](https://quarto.org) - Open-source scientific and technical publishing system
- **Theme**: Cosmo - Professional theme with clean typography and responsive design
- **Hosting**: GitHub Pages (deployed from `gh-pages` branch)
- **CI/CD**: GitHub Actions for automated rendering and deployment
- **Content Format**: Markdown (.qmd) with YAML front matter

## Repository Structure

```
cv/
├── .github/
│   └── workflows/
│       └── publish.yml          # GitHub Actions workflow for deployment
├── posts/                        # Blog posts directory
│   └── 2026-02-17-building-this-site/
│       └── index.qmd            # Each post in its own dated folder
├── _quarto.yml                  # Main Quarto configuration
├── index.qmd                    # CV homepage (three-image header, collapsible coursework)
├── blog.qmd                     # Blog listing page
├── styles.css                   # Custom CSS styling
├── chopra_maize_genetics_lab_logo.jpg  # Lab logo (used in three-image header)
├── Relevant Coursework.md       # Source for the coursework dropdown on the CV
├── .gitignore                   # Excludes build artifacts (_site/, .quarto/)
└── README.md                    # This file
```

### Generated Files (Not in Git)

```
├── .quarto/                     # Build cache
└── _site/                       # Rendered HTML (published to gh-pages branch)
```

## GitHub Pages Configuration

**Important**: GitHub Pages must be configured to deploy from the `gh-pages` branch:

1. Go to repository **Settings** → **Pages**
2. Under **Build and deployment** → **Source**:
   - Branch: `gh-pages` (not main)
   - Folder: `/ (root)`
3. Click **Save**

The GitHub Actions workflow automatically builds the site and pushes rendered HTML to the `gh-pages` branch. GitHub Pages then serves the static site from that branch.

## Content Management

### Updating Your CV

Edit `index.qmd` with your latest information. The page includes a collapsible **Relevant Coursework** dropdown at the bottom — to update it, edit the coursework list directly in `index.qmd` or keep `Relevant Coursework.md` as a reference and copy changes across.

```bash
# Edit the file
vim index.qmd

# Commit and push
git add index.qmd
git commit -m "Update CV with new research experience"
git push
```

The site will automatically rebuild and deploy within 1-2 minutes.

### Adding Blog Posts

Create a new post in the `posts/` directory using the date-slug naming convention:

```bash
# Create post directory
mkdir -p posts/YYYY-MM-DD-post-title

# Create the post file
touch posts/YYYY-MM-DD-post-title/index.qmd
```

**Post Template:**

```yaml
---
title: "Your Post Title"
subtitle: "Optional subtitle"
author: "Bailey M. Barenick"
date: "YYYY-MM-DD"
categories: [biotechnology, data-analysis, tutorial]
draft: false
---

## Introduction

Your content here...

## Code Examples

You can include R or Python code that executes:

\`\`\`{r}
# R code
data <- read.csv("data.csv")
summary(data)
\`\`\`

## Conclusion

Wrap up your post...
```

**Suggested Categories:**
- `research` - Research updates and findings
- `biotechnology` - Industry insights and methodologies
- `data-analysis` - R/Python analysis workflows
- `tutorial` - How-to guides
- `methods` - Lab protocols and techniques
- `visualization` - Data visualization and figures

### Adding Images to Posts

Store post-specific images in the post directory:

```bash
posts/YYYY-MM-DD-post-title/
├── index.qmd
├── preview.png          # Preview image for blog listing
├── figure1.png
└── data.csv
```

Reference images in your post:

```markdown
![Figure caption](figure1.png)
```

### Draft Posts

Set `draft: true` in the front matter to hide posts from the published site:

```yaml
---
title: "Work in Progress"
draft: true
---
```

## Local Development

### Prerequisites

Install Quarto from https://quarto.org/docs/get-started/

### Commands

```bash
# Preview site with live reload
quarto preview

# Render site to _site/ directory
quarto render

# Check Quarto installation
quarto check

# Publish to GitHub Pages (manual)
quarto publish gh-pages
```

**Note**: You don't need to run `quarto publish` manually - the GitHub Actions workflow handles deployment automatically when you push to main.

## Workflow

### Typical Development Cycle

1. **Make changes** to `index.qmd`, `blog.qmd`, or add new posts
2. **(Optional)** Preview locally: `quarto preview`
3. **Commit changes**: `git add . && git commit -m "Description"`
4. **Push to GitHub**: `git push`
5. **Automatic deployment**: GitHub Actions builds and publishes to gh-pages
6. **Site live** at https://baileymbbarenick.github.io/cv/ within 1-2 minutes

### Deployment Pipeline

```
Push to main → GitHub Actions triggers
              ↓
         Checkout code
              ↓
        Install Quarto
              ↓
      Render .qmd to HTML
              ↓
    Push to gh-pages branch
              ↓
    GitHub Pages deploys site
              ↓
         Site is live!
```

## Configuration

### _quarto.yml

The main configuration file controls site metadata, navigation, and appearance:

```yaml
project:
  type: website
  output-dir: _site

website:
  title: "Bailey M. Barenick"
  navbar:
    left:
      - text: "Home"
        href: index.qmd
      - text: "Blog"
        href: blog.qmd
      - icon: github
        href: https://github.com/BaileyMBarenick

format:
  html:
    theme: cosmo
    toc: true
```

**To customize:**
- Change `theme` to `flatly`, `sandstone`, `minty`, etc.
- Add pages to `navbar.left`
- Modify `toc-depth` for table of contents levels

### Blog Listing Configuration

In `blog.qmd`, control how posts are displayed:

```yaml
listing:
  contents: posts          # Directory containing posts
  sort: "date desc"        # Newest first
  type: default            # Layout: default, grid, or table
  categories: true         # Show category filters
  fields: [image, date, title, subtitle, categories, reading-time]
```

## Customization

### Styling

Edit `styles.css` to customize appearance:

```css
/* Example: Change heading colors */
h2 {
  border-bottom: 2px solid #007bff;
  color: #2c3e50;
}
```

### Theme Options

Available built-in themes (change in `_quarto.yml`):
- `cosmo` - Current theme, modern and clean
- `flatly` - Material design inspired
- `sandstone` - Warm, organic feel
- `minty` - Fresh, green accent
- `litera` - Google Fonts based
- `journal` - Academic style

See all themes: https://quarto.org/docs/output-formats/html-themes.html

## Advanced Features

### Adding Computational Content

Quarto can execute code and display results:

**R Example:**
```yaml
---
title: "Data Analysis"
format: html
---

\`\`\`{r}
#| echo: true
#| warning: false

library(ggplot2)
ggplot(mtcars, aes(x=wt, y=mpg)) +
  geom_point() +
  theme_minimal()
\`\`\`
```

**Python Example:**
```python
\`\`\`{python}
import pandas as pd
import matplotlib.pyplot as plt

data = pd.read_csv('data.csv')
plt.plot(data['x'], data['y'])
plt.show()
\`\`\`
```

### Adding New Pages

Create additional pages by adding `.qmd` files and updating navigation:

```yaml
# _quarto.yml
website:
  navbar:
    left:
      - text: "Home"
        href: index.qmd
      - text: "Blog"
        href: blog.qmd
      - text: "Publications"  # New page
        href: publications.qmd
```

## Troubleshooting

### Site Returns 404

- Verify GitHub Pages is set to deploy from `gh-pages` branch
- Check that GitHub Actions workflow completed successfully
- Wait 1-2 minutes after deployment completes

### Workflow Fails

```bash
# Check recent workflow runs
gh run list --limit 5

# View logs for a specific run
gh run view <run-id> --log
```

Common issues:
- Syntax errors in YAML front matter
- Missing required files
- Invalid date formats (must be YYYY-MM-DD)

### Local Preview Issues

```bash
# Verify Quarto installation
quarto check

# Clear cache and rebuild
rm -rf .quarto/ _site/
quarto render
```

## Resources

### Quarto Documentation
- [Official Docs](https://quarto.org/docs/)
- [Creating Websites](https://quarto.org/docs/websites/)
- [Blogging Guide](https://quarto.org/docs/websites/website-blog.html)
- [GitHub Pages Publishing](https://quarto.org/docs/publishing/github-pages.html)

### Tutorials
- [Adding a Blog to Quarto Website](https://samanthacsik.github.io/posts/2022-10-24-quarto-blogs/)
- [Ultimate Quarto Blog Guide](https://albert-rapp.de/posts/13_quarto_blog_writing_guide/13_quarto_blog_writing_guide.html)
- [Automating Quarto with GitHub Actions](https://thedatasavvycorner.com/blogs/03-quarto-github-actions)

### GitHub Actions
- [Quarto Actions Repository](https://github.com/quarto-dev/quarto-actions)
- [GitHub Pages Deployment](https://docs.github.com/en/pages)

## Maintenance

### Regular Tasks
- **Weekly**: Check for Quarto updates
- **Monthly**: Review GitHub Actions logs for issues
- **Quarterly**: Update CV content in `index.qmd`
- **Per post**: Add new blog posts to `posts/` directory

### Updating Content
- **CV updates**: Edit `index.qmd`
- **Blog posts**: Add to `posts/YYYY-MM-DD-slug/`
- **Navigation**: Update `_quarto.yml`
- **Styling**: Modify `styles.css`

## Future Enhancements

Potential additions for the site:

- [ ] Publications page with citation list
- [ ] Projects page with detailed case studies
- [ ] Search functionality (built into Quarto)
- [ ] Comments via GitHub Discussions/Giscus
- [ ] Dark mode theme toggle
- [ ] Google Analytics or privacy-friendly analytics
- [ ] RSS feed (automatic with Quarto blog)
- [ ] Custom domain (configure via CNAME)
- [ ] Interactive data visualizations with Observable JS
- [ ] PDF CV download option

## Contact

Bailey M. Barenick
MSc Candidate in Biotechnology
Pennsylvania State University
Chopra Maize Genetics Lab

GitHub: [@BaileyMBarenick](https://github.com/BaileyMBarenick)

## License

© 2026 Bailey M. Barenick. All rights reserved.
