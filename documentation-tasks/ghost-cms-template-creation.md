# Ghost CMS Template Creation

- [Ghost CMS Template Creation](#ghost-cms-template-creation)
  - [Getting Started](#getting-started)
    - [Installation and Setup](#installation-and-setup)
    - [Basic Configuration](#basic-configuration)
    - [Minimal Viable Theme](#minimal-viable-theme)
  - [Best Practices](#best-practices)
    - [Theme Structure and Organization](#theme-structure-and-organization)
    - [Design Patterns and Architecture](#design-patterns-and-architecture)
    - [Performance Optimization](#performance-optimization)
    - [Security Considerations](#security-considerations)
  - [Common Patterns and Examples](#common-patterns-and-examples)
    - [Template Basics](#template-basics)
    - [Content Templates](#content-templates)
    - [Advanced Template Techniques](#advanced-template-techniques)
  - [Troubleshooting](#troubleshooting)
    - [Common Errors and Solutions](#common-errors-and-solutions)
    - [Debugging Techniques](#debugging-techniques)
    - [Performance Issues](#performance-issues)
  - [Starter Projects and Templates](#starter-projects-and-templates)
    - [Official Ghost Starter Theme](#official-ghost-starter-theme)
    - [Other Starter Resources](#other-starter-resources)

## Getting Started

Ghost is a powerful, modern publishing platform that uses the Handlebars templating language for creating custom themes. This document provides a comprehensive guide to creating templates for Ghost CMS.

### Installation and Setup

Before you begin developing a Ghost theme, you'll need to set up your development environment:

1. **Install Ghost locally** (recommended for theme development):

   ```bash
   # Install Ghost-CLI globally
   npm install -g ghost-cli
   
   # Create a new directory and install Ghost
   mkdir ghost-local && cd ghost-local
   ghost install local
   ```

2. **Set up a theme development folder**:

   The best approach is to clone the official Starter theme:

   ```bash
   # Clone the Starter theme repository
   git clone https://github.com/TryGhost/Starter.git my-theme
   cd my-theme
   
   # Install dependencies
   npm install
   ```

3. **Link your theme to your local Ghost installation**:

   ```bash
   # Create a symbolic link to your Ghost themes directory
   ln -s /path/to/my-theme /path/to/ghost/content/themes/my-theme
   ```

4. **Restart Ghost and activate your theme** in the Ghost Admin panel under Settings → Design.

### Basic Configuration

Every Ghost theme requires specific configuration and files:

1. **package.json** - Contains theme metadata and configuration:

   ```json
   {
       "name": "my-ghost-theme",
       "description": "A custom theme for Ghost",
       "version": "1.0.0",
       "engines": {
           "ghost": ">=5.0.0"
       },
       "license": "MIT",
       "scripts": {
           "dev": "rollup -c --environment BUILD:development -w",
           "build": "rollup -c --environment BUILD:production",
           "zip": "npm run build && bestzip $npm_package_name.zip assets/* partials/* members/* *.hbs package.json"
       },
       "config": {
           "card_assets": true,
           "posts_per_page": 15,
           "image_sizes": {
               "xs": { "width": 100 },
               "s": { "width": 300 },
               "m": { "width": 600 },
               "l": { "width": 1200 },
               "xl": { "width": 2000 }
           }
       }
   }
   ```

2. **Required template files**:
   - `default.hbs` - The main template wrapper
   - `index.hbs` - Homepage template (post listings)
   - `post.hbs` - Individual post template

3. **Optional but recommended template files**:
   - `page.hbs` - Static page template
   - `tag.hbs` - Tag archive template
   - `author.hbs` - Author archive template
   - Custom templates: `page-{slug}.hbs`, `tag-{slug}.hbs`, etc.

### Minimal Viable Theme

Here's a breakdown of the minimum files needed for a functioning Ghost theme:

1. **default.hbs** - The base template that all other templates inherit from:

   ```handlebars
   <!DOCTYPE html>
   <html lang="{{@site.locale}}">
   <head>
       <meta charset="utf-8" />
       <meta name="viewport" content="width=device-width, initial-scale=1">
       <title>{{meta_title}}</title>
       {{ghost_head}}
   </head>
   <body class="{{body_class}}">
       <header>
           <a href="{{@site.url}}">{{@site.title}}</a>
           <nav>
               {{navigation}}
           </nav>
       </header>

       <main>
           {{{body}}}
       </main>

       <footer>
           <p>Published with <a href="https://ghost.org">Ghost</a></p>
       </footer>
       {{ghost_foot}}
   </body>
   </html>
   ```

2. **index.hbs** - The homepage template that displays post listings:

   ```handlebars
   {{!< default}}
   <div class="post-feed">
       {{#foreach posts}}
           <article class="post-card">
               <header>
                   <h2><a href="{{url}}">{{title}}</a></h2>
                   <time datetime="{{date format="YYYY-MM-DD"}}">{{date format="DD MMM YYYY"}}</time>
               </header>
               {{#if feature_image}}
                   <img src="{{feature_image}}" alt="{{title}}">
               {{/if}}
               <section class="post-excerpt">
                   <p>{{excerpt words="33"}}...</p>
                   <a href="{{url}}">Read more</a>
               </section>
           </article>
       {{/foreach}}
   </div>

   <div class="pagination">
       {{pagination}}
   </div>
   ```

3. **post.hbs** - The template for individual posts:

   ```handlebars
   {{!< default}}
   {{#post}}
   <article class="post">
       <header>
           <h1>{{title}}</h1>
           <time datetime="{{date format="YYYY-MM-DD"}}">{{date format="DD MMM YYYY"}}</time>
           <span>{{reading_time}}</span>
       </header>

       {{#if feature_image}}
           <figure>
               <img src="{{feature_image}}" alt="{{#if feature_image_alt}}{{feature_image_alt}}{{else}}{{title}}{{/if}}">
               {{#if feature_image_caption}}
                   <figcaption>{{feature_image_caption}}</figcaption>
               {{/if}}
           </figure>
       {{/if}}

       <section class="content">
           {{content}}
       </section>

       <footer>
           <div class="author">
               Written by {{#foreach authors}}<a href="{{url}}">{{name}}</a>{{/foreach}}
           </div>

           {{#if comments}}
           <section class="comments">
               {{comments}}
           </section>
           {{/if}}
       </footer>
   </article>
   {{/post}}
   ```

## Best Practices

### Theme Structure and Organization

A well-organized Ghost theme typically follows this directory structure:

```
theme-name/
├── assets/
│   ├── css/
│   ├── js/
│   └── images/
├── partials/
│   ├── header.hbs
│   ├── footer.hbs
│   ├── navigation.hbs
│   └── post-card.hbs
├── members/
│   ├── account.hbs
│   └── membership.hbs
├── default.hbs
├── index.hbs
├── post.hbs
├── page.hbs
├── tag.hbs
├── author.hbs
├── error.hbs
└── package.json
```

Best practices for organizing your theme:

1. **Use partials for reusable components** to keep your templates DRY (Don't Repeat Yourself)
2. **Separate concerns with directories** - JS, CSS, and images in the assets folder
3. **Naming conventions** - Use descriptive, consistent naming for all files
4. **Use comments** to document complex template logic

### Design Patterns and Architecture

Ghost themes use a template inheritance pattern:

1. **Template Inheritance** - All templates extend from `default.hbs` using `{{!< default}}`
2. **Context-Specific Templates** - Create custom templates for specific content:
   - `page-contact.hbs` for a `/contact/` page
   - `tag-news.hbs` for a `/tag/news/` archive
   - `author-jamie.hbs` for an `/author/jamie/` archive

3. **Helpers** - Use Ghost's built-in helpers for common tasks:
   - `{{#foreach}}` for iterating over collections
   - `{{#if}}` for conditional logic
   - `{{date}}` for formatting dates
   - `{{img_url}}` for responsive images

Example of template inheritance and partials:

```handlebars
{{!-- In default.hbs --}}
<header>
    {{> "header"}}
</header>

{{!-- In partials/header.hbs --}}
<div class="site-header">
    <a href="{{@site.url}}">
        {{#if @site.logo}}
            <img src="{{@site.logo}}" alt="{{@site.title}}">
        {{else}}
            {{@site.title}}
        {{/if}}
    </a>
    {{> "navigation"}}
</div>
```

### Performance Optimization

Optimize your Ghost theme for performance:

1. **Image optimization**:
   - Use responsive images with `{{img_url}}` helper
   - Specify multiple formats (WebP, AVIF)
   - Use appropriate sizes attribute

   ```handlebars
   <picture>
     <source 
       srcset="
       {{img_url feature_image size="s" format="avif"}} 300w,
       {{img_url feature_image size="m" format="avif"}} 600w,
       {{img_url feature_image size="l" format="avif"}} 1200w"
       sizes="(max-width: 1000px) 100vw, 1000px" 
       type="image/avif">
     <img
       srcset="
       {{img_url feature_image size="s"}} 300w,
       {{img_url feature_image size="m"}} 600w,
       {{img_url feature_image size="l"}} 1200w"
       sizes="(max-width: 1000px) 100vw, 1000px" 
       src="{{img_url feature_image size="m"}}"
       alt="{{title}}">
   </picture>
   ```

2. **Asset optimization**:
   - Bundle and minify CSS and JavaScript
   - Use deferred or async loading for non-critical scripts
   - Use modern build tools like Rollup (included in Starter theme)

3. **Lazy loading**:
   - Use native lazy loading for images: `loading="lazy"`
   - Implement infinite scroll or "load more" for content pagination

### Security Considerations

Keep your Ghost theme secure:

1. **Context-specific escaping** - Handlebars automatically escapes values, but be cautious with triple braces `{{{content}}}`
2. **Be cautious with user-generated content**
3. **Follow Ghost's security guidelines**
4. **Keep dependencies updated** - Regularly update npm packages
5. **Validate your theme** with GScan to catch security issues

## Common Patterns and Examples

### Template Basics

1. **Site Header**:

   ```handlebars
   <header class="site-header">
       <div class="container">
           <div class="site-logo">
               {{#if @site.logo}}
                   <a href="{{@site.url}}"><img src="{{@site.logo}}" alt="{{@site.title}}"></a>
               {{else}}
                   <a href="{{@site.url}}">{{@site.title}}</a>
               {{/if}}
           </div>
           <nav class="site-nav">
               {{navigation}}
           </nav>
       </div>
   </header>
   ```

2. **Post Card** (for listings):

   ```handlebars
   {{!-- partials/post-card.hbs --}}
   <article class="post-card {{post_class}}">
       {{#if feature_image}}
       <a class="post-card-image-link" href="{{url}}">
           <img class="post-card-image" 
                src="{{img_url feature_image size="m"}}"
                alt="{{title}}" 
                loading="lazy">
       </a>
       {{/if}}
       <div class="post-card-content">
           <a class="post-card-content-link" href="{{url}}">
               <header class="post-card-header">
                   {{#if primary_tag}}
                   <div class="post-card-tags">{{primary_tag.name}}</div>
                   {{/if}}
                   <h2 class="post-card-title">{{title}}</h2>
               </header>
               <div class="post-card-excerpt">
                   <p>{{excerpt words="33"}}</p>
               </div>
           </a>
           <footer class="post-card-meta">
               <time datetime="{{date format="YYYY-MM-DD"}}">
                   {{date format="D MMM YYYY"}}
               </time>
               <span class="reading-time">{{reading_time}}</span>
           </footer>
       </div>
   </article>
   ```

3. **Using the Post Card Partial**:

   ```handlebars
   {{!-- In index.hbs --}}
   <div class="post-feed">
       {{#foreach posts}}
           {{> "post-card"}}
       {{/foreach}}
   </div>
   ```

### Content Templates

1. **Basic Post Template**:

   ```handlebars
   {{!< default}}
   {{#post}}
   <article class="post-full {{post_class}}">
       <header class="post-full-header">
           {{#if primary_tag}}
           <div class="post-full-tags">
               <a href="{{primary_tag.url}}">{{primary_tag.name}}</a>
           </div>
           {{/if}}
           <h1 class="post-full-title">{{title}}</h1>
           <div class="post-full-meta">
               <time datetime="{{date format="YYYY-MM-DD"}}">
                   {{date format="D MMMM YYYY"}}
               </time>
               <span class="reading-time">{{reading_time}}</span>
           </div>
       </header>

       {{#if feature_image}}
       <figure class="post-full-image">
           <img src="{{img_url feature_image size="xl"}}" 
                alt="{{#if feature_image_alt}}{{feature_image_alt}}{{else}}{{title}}{{/if}}">
           {{#if feature_image_caption}}
               <figcaption>{{feature_image_caption}}</figcaption>
           {{/if}}
       </figure>
       {{/if}}

       <section class="post-full-content">
           <div class="post-content">
               {{content}}
           </div>
       </section>

       <footer class="post-full-footer">
           <div class="author-list">
               {{#foreach authors}}
               <div class="author-card">
                   {{#if profile_image}}
                   <img class="author-profile-image" 
                        src="{{img_url profile_image size="xs"}}" 
                        alt="{{name}}">
                   {{/if}}
                   <div class="author-info">
                       <h5>{{name}}</h5>
                       {{#if bio}}
                           <p>{{bio}}</p>
                       {{/if}}
                   </div>
               </div>
               {{/foreach}}
           </div>
       </footer>

       {{#if comments}}
       <section class="post-full-comments">
           {{comments}}
       </section>
       {{/if}}
   </article>
   {{/post}}
   ```

2. **Page Template**:

   ```handlebars
   {{!< default}}
   {{#post}}
   <article class="page-full {{post_class}}">
       <header class="page-full-header">
           <h1 class="page-full-title">{{title}}</h1>
       </header>

       {{#if feature_image}}
       <figure class="page-full-image">
           <img src="{{img_url feature_image size="xl"}}" 
                alt="{{#if feature_image_alt}}{{feature_image_alt}}{{else}}{{title}}{{/if}}">
       </figure>
       {{/if}}

       <section class="page-full-content">
           <div class="page-content">
               {{content}}
           </div>
       </section>
   </article>
   {{/post}}
   ```

### Advanced Template Techniques

1. **Custom Post Featured Layout** (for specific tags):

   ```handlebars
   {{!-- For a page like tag-featured.hbs --}}
   {{!< default}}
   <div class="featured-header">
       <h1>{{tag.name}}</h1>
       <p>{{tag.description}}</p>
   </div>

   <div class="featured-grid">
       {{#foreach posts}}
           <div class="featured-item {{#if @first}}featured-main{{/if}}">
               <a href="{{url}}">
                   <div class="featured-image" style="background-image: url({{img_url feature_image size='m'}})"></div>
                   <div class="featured-content">
                       <h2>{{title}}</h2>
                       {{#if @first}}
                           <p>{{excerpt words="25"}}</p>
                       {{/if}}
                   </div>
               </a>
           </div>
       {{/foreach}}
   </div>
   ```

2. **Related Posts** (in post.hbs):

   ```handlebars
   <div class="related-posts">
       <h3>Related Posts</h3>
       <div class="related-post-grid">
           {{#get "posts" filter="tags:[{{primary_tag.slug}}]+id:-{{id}}" limit="3" as |related|}}
               {{#foreach related}}
                   <div class="related-post-card">
                       {{#if feature_image}}
                       <a class="related-post-image" href="{{url}}">
                           <img src="{{img_url feature_image size="s"}}" alt="{{title}}">
                       </a>
                       {{/if}}
                       <div class="related-post-content">
                           <h4><a href="{{url}}">{{title}}</a></h4>
                           <time datetime="{{date format="YYYY-MM-DD"}}">
                               {{date format="D MMM YYYY"}}
                           </time>
                       </div>
                   </div>
               {{/foreach}}
           {{/get}}
       </div>
   </div>
   ```

3. **Dynamic Content Zones**:

   ```handlebars
   {{!-- Using the {{#match}} helper for dynamic content --}}
   {{#post}}
       {{#match featured "==" true}}
           <div class="featured-banner">
               <span>Featured Post</span>
           </div>
       {{/match}}
   {{/post}}
   ```

## Troubleshooting

### Common Errors and Solutions

1. **GScan Validation Errors**:

   | Error | Solution |
   |-------|----------|
   | "Template file not found: default.hbs" | Ensure your theme includes the required default.hbs file |
   | "The asset helper must take a minimum of 1 arguments" | Check your asset helper syntax: `{{asset "css/style.css"}}` |
   | "The ghost_head helper should be the last item in the head of the template" | Move the `{{ghost_head}}` helper to the end of your `<head>` section |
   | "Missing package.json file" | Create a valid package.json with required Ghost theme metadata |

2. **Rendering Issues**:

   | Issue | Solution |
   |-------|----------|
   | Content not displaying | Check you're using the correct context (e.g., `{{#post}}` in post.hbs) |
   | Images not loading | Verify image paths and ensure `{{img_url}}` helper is used correctly |
   | Helpers not working | Check helper syntax and ensure you're using them in the correct context |
   | Custom CSS not applying | Verify your asset links and build process is working correctly |

### Debugging Techniques

1. **Use GScan to validate your theme**:

   ```bash
   # Install GScan globally
   npm install -g gscan
   
   # Test your theme
   gscan /path/to/your/theme
   
   # Or use the online version at https://gscan.ghost.org/
   ```

2. **Check Ghost error logs** in your Ghost installation directory:

   ```bash
   # View logs
   ghost ls
   
   # If errors occur
   ghost doctor
   ```

3. **Debug Handlebars templates**:

   - Use `{{log variable}}` to output variables to the console
   - Inspect element in your browser to see rendered HTML
   - Create debugging helpers to visualize context

   ```handlebars
   {{!-- Create a debug helper in your theme --}}
   <script>
   {{#if @debug}}
       console.log('Context:', {{{json this}}});
   {{/if}}
   </script>
   ```

### Performance Issues

1. **Slow page loading**:
   - Optimize images using responsive sizing and formats
   - Minimize HTTP requests by combining CSS/JS files
   - Use browser caching with proper cache headers

2. **High resource usage**:
   - Reduce complex Handlebars logic
   - Optimize database queries with proper limits
   - Defer non-critical resources

3. **Mobile performance**:
   - Ensure your theme is fully responsive
   - Test on real mobile devices
   - Use tools like Lighthouse to identify mobile-specific issues

## Starter Projects and Templates

### Official Ghost Starter Theme

The [Ghost Starter Theme](https://github.com/TryGhost/Starter) is the official development framework for creating Ghost themes. It includes:

- Modern JavaScript with ESM
- Asset optimization with Rollup
- Live reload during development
- PostCSS for modern CSS features
- GitHub Actions for deployment

To start with the official Starter theme:

```bash
# Clone the repository
git clone https://github.com/TryGhost/Starter.git my-theme
cd my-theme

# Install dependencies
npm install

# Start development mode with live reload
npm run dev

# Build for production
npm run build

# Create a distributable zip
npm run zip
```

Key features of the Starter theme:

- Minimal, clean design as a foundation
- Responsive layout ready for customization
- All required Ghost theme files and structure
- Modern development workflow with hot reloading
- Optimized asset pipeline

### Other Starter Resources

1. **Casper** - Ghost's default theme is a great reference:
   - [GitHub: TryGhost/Casper](https://github.com/TryGhost/Casper)
   - Well-documented code with excellent patterns to follow
   - Full-featured theme with all common components

2. **Community Themes** for inspiration:
   - [Ghost Marketplace](https://ghost.org/marketplace/)
   - [ThemeForest Ghost Themes](https://themeforest.net/category/cms-themes/ghost-themes)

3. **Development Tools**:
   - [Ghost VS Code Extension](https://marketplace.visualstudio.com/items?itemName=TryGhost.ghost)
   - [GScan](https://gscan.ghost.org/) - Theme validation tool
   - [Ghost CLI](https://ghost.org/docs/ghost-cli/) - Command-line interface for Ghost