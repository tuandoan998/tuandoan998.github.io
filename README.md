# My Portfolio Website

This is a personal portfolio and blog site based on a GitHub Pages template.

## Content Management

### How to Create a New Blog Post

To add a new blog post, you just need to create a new Markdown file in the `_posts/` directory.

#### Naming Convention
The filename **must** follow this format:
`YYYY-MM-DD-title-of-post.md`

Example: `2024-05-12-my-new-project.md`

#### Front Matter (Metadata)
At the top of your markdown file, you should include the YAML front matter which specifies how the post is rendered. Here is an example:

```yaml
---
title: 'My New Project'
date: 2024-05-12
permalink: /posts/2024/05/my-new-project/
tags:
  - project
  - update
---
```

After the `---`, you can write your blog post using standard Markdown!

### Editing Portfolios and CV
- **Portfolio**: You can find portfolio items in the `_portfolio/` directory. They act similar to posts.
- **CV Page**: You can edit `_pages/cv.md` or provide a direct link to your PDF resume.
- **About Me**: The main landing page is managed via `_pages/about.md`.

## Running Locally

1. Install Ruby and Jekyll dependencies:
   ```bash
   bundle install
   ```
2. Serve the site locally:
   ```bash
   bundle exec jekyll serve -l -H localhost
   ```

For advanced instructions or framework modifications, consult the original template docs at [academicpages.github.io](https://academicpages.github.io/).
