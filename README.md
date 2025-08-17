# Zeus's Security Blog

A personal blog focused on offensive security, ethical hacking, and cybersecurity certifications. Built with Hugo and the Terminal theme.

## Features

- Custom Terminal theme with personalized colors
- Responsive design
- Full-width layout
- Content organized by categories (cheat sheets, methodologies, scripts, tools)
- OSCP certification resources and write-ups

## Local Development

### Prerequisites

- [Hugo Extended](https://gohugo.io/getting-started/installing/) (v0.92.2 or later)
- Git

### Setup

1. Clone this repository:
   ```bash
   git clone https://github.com/lightninggod7/lightninggod7.github.io.git
   cd lightninggod7.github.io
   ```

2. Update submodules to get the theme:
   ```bash
   git submodule update --init --recursive
   ```

3. Start the Hugo development server:
   ```bash
   hugo server -D
   ```

4. Visit http://localhost:1313/ in your browser

### Creating New Content

```bash
# Create a new post
hugo new posts/category-name/post-name.md
```

## Deployment

This site is deployed using GitHub Pages. Any push to the main branch will trigger a GitHub Action to build and deploy the site.

## Theme Customization

The Terminal theme has been customized with the following colors:
- Background: rgb(26, 23, 15)
- Foreground: rgb(236, 234, 229)
- Accent: rgb(238, 195, 94)

Custom styles are defined in `assets/css/custom.css`.

## License

This project is licensed under the MIT License - see the LICENSE file for details.