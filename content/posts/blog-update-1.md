---
title: "Blog Update 1"
date: 2026-01-31T00:59:03+05:30
draft: false
tags: [blog-update]
description: "The first post of this blog; entails how I made this blog and my intentions for it."
---

# Hello, World!

# Backstory

After much procrastination and a couple of over-ambitious attempts, I have finally set up a blog.

I had decided to use hugo from the start, but the first couple of attempts had me trying to use it from scratch instead of using a template. That didn't go very well. After a couple of days of trying to figure out documentation, I lost interest and found the next shiny object to tinker with. 

What worked this time was deciding to use a template to get an MVP(what am I selling here?!) out and then deciding to iterate on it. Whether this will work out or not, we will find out in the future.

# How to make a blog exactly like this one

There are enough tutorials online (better than this one!) on how to make a blog using hugo. But if you're interested in how to make this blog exactly, the next part of this blog will be a tutorial-like description of exactly what I did to make this. [Skip to next section](#plans).

Here are the detailed steps to create your Hugo blog with PaperMod:

## 1. Install Hugo

**macOS:**
```bash
brew install hugo
```

**Linux (Ubuntu/Debian):**
```bash
sudo apt-get install hugo
```

**Windows:**
```bash
choco install hugo-extended
```

Or download from [Hugo releases](https://github.com/gohugoio/hugo/releases)

Verify installation:
```bash
hugo version
```

## 2. Create Your Blog

```bash
# Create new site
hugo new site my-blog
cd my-blog
```

```bash
# Initialize git repository
git init
```

## 3. Install PaperMod Theme

Add theme as submodule

```bash
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```
Update the submodule

```bash
git submodule update --init --recursive
```

## 4. Configure Your Blog

I deleted the default `hugo.toml` and used a `config.yml` file instead:

```bash
rm hugo.toml
nvim config.yml
```

Create `config.yml` with this basic configuration:

```yaml
baseURL: "https://yourdomain.com/"
title: "My Blog"
theme: "PaperMod"
languageCode: "en-us"

enableRobotsTXT: true
buildDrafts: false
buildFuture: false
buildExpired: false

minify:
  disableXML: true
  minifyOutput: true

params:
  env: production
  title: "My Blog"
  description: "Your blog description here"
  author: "Your Name"
  
  # Theme settings
  defaultTheme: auto # auto, light, dark
  disableThemeToggle: false
  hideFooter: true
  
  ShowReadingTime: true
  ShowShareButtons: true
  ShowPostNavLinks: true
  ShowBreadCrumbs: true
  ShowCodeCopyButtons: true
  ShowWordCount: true
  
  homeInfoParams:
    Title: "Welcome 👋"
    Content: "A short description of your blog"

  socialIcons:
    - name: github
      url: "https://github.com/yourusername"
    - name: twitter
      url: "https://twitter.com/yourusername"

menu:
  main:
    - identifier: posts
      name: Posts
      url: /posts/
      weight: 10
    - identifier: tags
      name: Tags
      url: /tags/
      weight: 20
    - identifier: about
      name: About
      url: /about/
      weight: 30
```

## 5. Customize Colors and Fonts

Create `assets/css/extended/custom.css`:

```bash
mkdir -p assets/css/extended
nvim assets/css/extended/custom.css
```

Add to `assets/css/extended/custom.css`:

```css
/* Import custom font */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');

/* ============================================
   LIGHT MODE COLORS
   ============================================ */
:root {
  /* Main background */
  --theme: #110b2b;

  /* Card/Entry background */
  --entry: #f5f5f5;

  /* Primary text color */
  --primary: #1a1a1a;

  /* Secondary/muted text */
  --secondary: #666666;

  /* Link/accent color */
  --tertiary: #ff6b35;

  /* Borders */
  --border: #e8e8e8;

  /* Code block background */
  --code-bg: #f0f0f0;

  /* Hover background */
  --hljs-bg: #fafafa;
}

/* ============================================
   DARK MODE COLORS
   ============================================ */
.dark {
  --theme: #110b2b;

  --entry: #161b22;

  --primary: #e6edf3;

  --secondary: #8b949e;

  --tertiary: #ff8c5a;

  --border: #30363d;

  --code-bg: #1c2128;

  --hljs-bg: #21262d;
}

/* ============================================
   GLOBAL STYLES
   ============================================ */

/* Apply custom font */
body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

/* Smooth transitions when switching themes */
body,
.main,
.post-entry,
.post-single {
  transition: background-color 0.3s ease, color 0.3s ease, border-color 0.3s ease;
}

/* Improve line height for readability */
.post-content p,
.post-content li,
article p,
article li {
  line-height: 1.7;
}

/* Better heading styles */
h1,
h2,
h3,
h4,
h5,
h6 {
  font-weight: 600;
}

/* Subtle shadow for cards in light mode */
:root .post-entry {
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
}

.dark .post-entry {
  box-shadow: none;
}

/* Rounded corners for code blocks */
pre,
code {
  border-radius: 6px;
}

/* Link hover effect */
a {
  transition: opacity 0.2s ease;
}

a:hover {
  opacity: 0.8;
}

```

## 6. Create Your First Post

```bash
hugo new posts/my-first-post.md
```

Edit `content/posts/my-first-post.md`:

```markdown
---
title: "My First Post"
date: 2026-01-30
draft: false
tags: ["hello", "first-post"]
---

This is my first blog post!

## Welcome

Here's some content...
```

## 7. Create an About Page

```bash
hugo new about.md
```

Edit `content/about.md`:

```markdown
---
title: "About"
url: "/about/"
---

Information about you and your blog.
```

## 8. Test Locally

Start development server

```bash
hugo server -D
```
Or without drafts

```bash
hugo server
```

Visit `http://localhost:1313` to see your blog.

## 9. Build for Production

```bash
hugo
```

This creates a `public/` folder with your static site.

## 10. Deploying
At the moment, the site is deployed on netlify.
```bash
git add .
git commit -m "Initial commit"
gh repo create my-blog --public --source=. --push
```
I had initially learnt how to use git using The Odin Project's guide for the same, so I didn't know about the GitHub CLI. Now I can create new repos on GitHub without leaving the terminal!

Onto setting up netlify.
1. Sign up for Netlify

    Go to https://netlify.com
    Click "Sign up"
    Choose "Sign up with GitHub"
    Authorize Netlify to access your GitHub account

2. Import Your Site

    Click "Add new site" (or "Import an existing project")
    Click "Import from Git"
    Choose "GitHub"
    Authorize Netlify if prompted
    Search for and select your blog repository (e.g., "my-blog")

3. Configure Build Settings Netlify should auto-detect Hugo, but verify:

    Branch to deploy: main
    Build command: hugo
    Publish directory: public

Click "Show advanced" and add environment variable:

    Key: HUGO_VERSION
    Value: Your Hugo version (check with hugo version - use just the number like 0.152.2)

4. Deploy Site

    Click "Deploy [site-name]"
    Wait 1-2 minutes for build to complete
    Click the site URL when it shows "Published"

5. (Optional) Rename Your Site

    Go to "Site settings" → "General" → "Site details"
    Click "Change site name"
    Enter a custom name (e.g., yourname-blog)
    Your URL becomes: yourname-blog.netlify.app

Future Deploys

Every time you push to GitHub:
```bash
git add .
git commit -m "Your changes"
git push
```

Netlify automatically rebuilds and deploys. No manual steps needed!
Troubleshooting

    Build fails: Check HUGO_VERSION is set correctly
    Changes not showing: Hard refresh browser (Ctrl+Shift+R)
    404 errors: Check baseURL in config.yml matches your Netlify URL



## Quick Customization Reference

**Change colors:** Edit `assets/css/extended/custom.css`

**Change fonts:** Add Google Fonts link to `layouts/partials/extend_head.html` and update CSS

**Add features:** Modify `params` in `config.yml`

**Add menu items:** Update `menu.main` in `config.yml`

The [PaperMod documentation](https://github.com/adityatelange/hugo-PaperMod/wiki) has detailed guides for advanced customization like adding comments, analytics, search, and more.

## Changes I made:

- I added a favicon made using [favicon.io](favicon.io).
- Changed the archetypes from toml to yml.

I am writing this at *2 am*, so if there are any questions or clarifications, please reach out on my [twitter](https://twitter.com/skdooshdev).

# Plans
My plans for this blog are simple - building in public and getting better at writing.

I plan to do two posts a week, which will either be update posts or project showcase posts.


Thanks for reading!
