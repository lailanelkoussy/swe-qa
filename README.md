# SWE-QA Project Website (gh-pages branch)

This branch contains the Jekyll-based GitHub Pages site for the SWE-QA project.

## Local Development

To run the site locally:

```bash
# Install dependencies
bundle install

# Serve the site
bundle exec jekyll serve

# View at http://localhost:4000/swe-qa/
```

## Structure

```
.
├── _config.yml          # Jekyll configuration
├── _layouts/            # Page layouts
├── _includes/           # Reusable components (header, footer)
├── assets/              # Static assets (CSS, images, PDFs)
├── paper/               # Paper PDF
├── index.html           # Homepage
├── Gemfile              # Ruby dependencies
└── .gitignore          # Git ignore rules
```

## Deployment

This site is automatically deployed by GitHub Pages when changes are pushed to the `gh-pages` branch.

**Site URL:** https://lailanelkoussy.github.io/swe-qa/

## Main Repository

For datasets and full project documentation, see the `main` branch:
https://github.com/lailanelkoussy/swe-qa

---

© 2026 Laila El Koussy. LREC-COLING 2026.
