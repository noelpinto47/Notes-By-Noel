# Notes By Noel 🌱

A warm, welcoming documentation site where I document my technological journey. Built with Jekyll and the Just the Docs theme, featuring a soothing green color palette designed for comfortable reading and learning.

## 🎯 About

This is my personal knowledge base—a collection of notes, resources, and insights gathered throughout my journey in technology. It serves as both a reference for myself and a resource for others who might find it helpful.

## ✨ Features

- 🎨 **Warm Green Theme** - Soft, educational color scheme easy on the eyes
- 🔍 **Full-Text Search** - Quickly find what you need
- 📱 **Responsive Design** - Works beautifully on all devices
- 🗂️ **Organized Structure** - Topics grouped logically for easy navigation
- 🚀 **Fast & Simple** - Static site for lightning-fast load times

## 🛠️ Tech Stack

- **Jekyll** - Static site generator
- **Just the Docs** - Documentation theme
- **GitHub Pages** - Hosting (optional)
- **Custom SCSS** - Warm green color scheme

## 🚀 Getting Started

### Prerequisites

- Ruby (2.7 or higher)
- Bundler (`gem install bundler`)

### Local Development

1. Clone the repository:
   ```bash
   git clone https://github.com/noelpinto47/notes-by-noel.git
   cd notes-by-noel
   ```

2. Install dependencies:
   ```bash
   bundle install
   ```

3. Run the local server:
   ```bash
   bundle exec jekyll serve
   ```

4. Visit `http://localhost:4000` in your browser

### Making Changes

1. Add new documentation files in the `_docs/` directory
2. Use proper front matter for navigation:
   ```yaml
   ---
   layout: default
   title: Your Page Title
   parent: Parent Page (if any)
   nav_order: 1
   ---
   ```

3. Save and the site will auto-reload (if using `--livereload`)

## 📁 Project Structure

```
notes-by-noel/
├── _config.yml              # Site configuration
├── _docs/                   # Documentation pages
│   ├── getting-started.md
│   └── programming/
│       ├── index.md
│       └── python-basics.md
├── _sass/                   # Custom styles
│   ├── color_schemes/
│   │   └── warm_green.scss # Custom color theme
│   └── custom/
│       └── custom.scss      # Additional custom styles
├── index.md                 # Homepage
└── README.md               # This file
```

## 🎨 Theme Customization

The warm green theme is defined in `_sass/color_schemes/warm_green.scss`. Key colors:

- **Primary Green**: `#4a8f4a` - Links and primary actions
- **Light Green**: `#e8f4e8` - Subtle backgrounds
- **Dark Green**: `#2d5f2d` - Emphasis and headings

Additional styling customizations are in `_sass/custom/custom.scss`.

## 📝 Contributing

While this is a personal documentation site, suggestions and corrections are welcome!

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📄 License

This project is open source and available under the MIT License.

## 🤝 Acknowledgments

- Built with [Jekyll](https://jekyllrb.com/)
- Theme: [Just the Docs](https://just-the-docs.github.io/just-the-docs/)
- Inspired by the tech community's culture of sharing knowledge

---

Made with ☕ and curiosity | © 2025 Noel Pinto
