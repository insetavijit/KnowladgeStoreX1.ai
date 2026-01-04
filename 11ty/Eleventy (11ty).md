### **[[01 Fundamentals (11ty)]] **

Master Eleventy as the simple, powerful static site generator for building blazing-fast websites. Learn zero-config setup, template languages, and core concepts. Understand why 11ty is loved by developers—no JavaScript frameworks required, works with your existing directory structure, and builds incredibly fast sites. Downloaded 15+ million times and used on 82,000+ GitHub repositories, 11ty is the modern choice for static sites. Essential for JAMstack development and modern web projects.

| Topic                            | Focus & Purpose                                                                                                                                                             |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **[[1.1 Installation & Setup]]** | Installing 11ty (npm install @11ty/eleventy); Node.js requirements; project initialization; directory structure; first site; zero-config start. Getting started.            |
| **[[1.2 Template Languages]]**   | Supported languages (HTML, Markdown, Nunjucks, Liquid, Handlebars, JavaScript, Pug, EJS, Haml, Mustache, WebC); choosing templates; mixing languages. Language flexibility. |
| **[[1.3 Project Structure]]**    | Input/output directories; folder organization; includes; layouts; data folders; static files; best practices. Organizing projects.                                          |
| **[[1.4 Configuration File]]**   | eleventy.config.js; configuration options; zero-config vs custom; ESM vs CommonJS; async configuration; returns object. Project configuration.                              |
| **[[1.5 Command Line Usage]]**   | Build command; serve command; watch mode; incremental builds; dry run; quiet mode; CLI options. Running 11ty.                                                               |
| **[[1.6 Front Matter]]**         | YAML front matter; data in templates; custom data; computed data; front matter formats; data priority. Template metadata.                                                   |
| **[[1.7 Permalinks]]**           | Permalink structure; custom URLs; permalink variables; date-based permalinks; pagination permalinks; dynamic permalinks. URL control.                                       |
| **[[1.8 Why 11ty?]]**            | Speed comparison; simplicity; flexibility; no client JS; incremental adoption; framework agnostic; long-term thinking. Value proposition.                                   |

### **[[2 Layouts & Templates]]**

Master 11ty's powerful layout and templating system. Learn layout chaining, template inheritance, partials, and includes. Understand different template engines and when to use each. Build reusable, maintainable templates. Layouts provide the foundation for consistent, DRY (Don't Repeat Yourself) site architecture.

| Topic                            | Focus & Purpose                                                                                                                   |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **[[2.1 Layout Basics]]**        | Creating layouts; layout directory; assigning layouts; front matter layout; layout chaining; default layouts. Template structure. |
| **[[2.2 Template Inheritance]]** | Extending layouts; nested layouts; layout chains; content blocks; overriding sections. Layout hierarchy.                          |
| **[[2.3 Nunjucks Templates]]**   | Nunjucks syntax; variables; filters; macros; includes; conditionals; loops; Nunjucks advantages. Popular choice.                  |
| **[[2.4 Liquid Templates]]**     | Liquid syntax; tags; filters; objects; Jekyll compatibility; when to use Liquid. Alternative engine.                              |
| **[[2.5 Markdown Processing]]**  | Markdown basics; Markdown-it; plugins; syntax extensions; markdown-it-anchor; code highlighting. Content format.                  |
| **[[2.6 Includes & Partials]]**  | Include files; reusable components; relative includes; include parameters; partial organization. Modular templates.               |
| **[[2.7 WebC Components]]**      | WebC introduction; component syntax; web components; props; slots; WebC advantages. Modern components.                            |
| **[[2.8 JavaScript Templates]]** | .11ty.js files; template literals; JSX-like syntax; dynamic generation; JS advantages. Programmatic templates.                    |

### **[[3 Collections & Data]]**

Master 11ty's data cascade and collection system. Learn creating collections, filtering, sorting, and pagination. Understand global data, directory data, and template data. Build dynamic site structures from data. Collections and data management enable sophisticated content organization and generation.

| Topic                            | Focus & Purpose                                                                                                                   |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **[[3.1 Collections Basics]]**   | Creating collections; tags; collections.all; automatic collections; custom collections; collection items. Content grouping.       |
| **[[3.2 Collection Filtering]]** | Filter functions; advanced filtering; filtering by date; filtering by custom fields; multiple filters. Selective content.         |
| **[[3.3 Sorting Collections]]**  | Sort methods; custom sorting; reverse sort; sort by date; sort by custom fields. Ordering content.                                |
| **[[3.4 Data Cascade]]**         | Data priority; template data; directory data; global data; front matter data; computed data. Data hierarchy.                      |
| **[[3.5 Global Data Files]]**    | _data directory; JSON data; JavaScript data files; fetching external data; async data; data caching. Site-wide data.              |
| **[[3.6 Directory Data]]**       | Directory-specific data; JSON files; JavaScript files; inheriting data; overriding data. Scoped data.                             |
| **[[3.7 Computed Data]]**        | Computed properties; dynamic values; accessing other data; eleventyComputed; use cases. Derived data.                             |
| **[[3.8 Pagination]]**           | Pagination basics; paginated collections; pagination size; pagination aliases; generating pages from data. Multi-page generation. |

### **[[4 Content Management]]**

Master content creation, organization, and management in 11ty. Learn blog setup, taxonomies, tags, dates, and content strategies. Build blogs, documentation sites, and content-rich applications. Proper content management enables scalable, maintainable sites with excellent content discovery.

| Topic                            | Focus & Purpose                                                                                                    |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **[[4.1 Blog Setup]]**           | Blog structure; post organization; post collections; post templates; blog index; archive pages. Building blogs.    |
| **[[4.2 Tags & Taxonomies]]**    | Tag systems; multiple tags; tag pages; category systems; filtering by tags; tag clouds. Content classification.    |
| **[[4.3 Content Dates]]**        | Date handling; content dates; created dates; published dates; date formatting; date sorting. Temporal content.     |
| **[[4.4 Draft Posts]]**          | Draft system; conditional rendering; excluding drafts; preview drafts; draft workflow. Content staging.            |
| **[[4.5 Featured Content]]**     | Featured flags; highlighting content; featured collections; homepage features; custom ordering. Content promotion. |
| **[[4.6 Search Functionality]]** | Client-side search; Lunr.js; Pagefind; search indexes; search UI; search optimization. Site search.                |
| **[[4.7 RSS Feeds]]**            | RSS plugin; feed generation; Atom feeds; JSON feeds; podcast feeds; feed templates. Content syndication.           |
| **[[4.8 Sitemap Generation]]**   | Sitemap plugin; XML sitemap; sitemap configuration; dynamic sitemaps; robots.txt. SEO basics.                      |

### **[[5 Plugins & Extensions]]**

Master 11ty's plugin ecosystem and create custom plugins. Learn official plugins, community plugins, and plugin development. Extend 11ty with images, syntax highlighting, navigation, and custom functionality. Plugins dramatically extend 11ty's capabilities without framework bloat.

| Topic                               | Focus & Purpose                                                                                                                      |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **[[5.1 Plugin Basics]]**           | Installing plugins; plugin configuration; official plugins; community plugins; plugin patterns. Extending 11ty.                      |
| **[[5.2 Image Plugin]]**            | @11ty/eleventy-plugin-image; image optimization; responsive images; image formats; lazy loading; image shortcodes. Optimized images. |
| **[[5.3 Syntax Highlighting]]**     | Syntax highlighting plugin; PrismJS; code block styling; language support; line highlighting. Code display.                          |
| **[[5.4 Navigation Plugin]]**       | Navigation plugin; hierarchical navigation; breadcrumbs; nav structure; active states. Site navigation.                              |
| **[[5.5 Fetch Plugin]]**            | Fetching remote data; caching; API integration; async fetch; fetch at build time. External data.                                     |
| **[[5.6 RSS Plugin]]**              | Generating RSS feeds; feed configuration; item templates; podcast RSS; multiple feeds. Syndication feeds.                            |
| **[[5.7 i18n Plugin]]**             | Internationalization; multi-language sites; locale management; translated content; language switching. Multilingual sites.           |
| **[[5.8 Creating Custom Plugins]]** | Plugin architecture; plugin functions; filters; shortcodes; transforms; collections; plugin distribution. Building plugins.          |

### **[[6 Filters, Shortcodes & Transforms]]**

Master 11ty's data transformation and templating utilities. Learn creating filters, shortcodes, and transforms. Build reusable template logic and content processing. These tools enable powerful template functionality while keeping markup clean and maintainable.

| Topic                            | Focus & Purpose                                                                                                          |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| **[[6.1 Filter Basics]]**        | Built-in filters; template filters; universal filters; async filters; filter patterns. Data transformation.              |
| **[[6.2 Custom Filters]]**       | Creating filters; date filters; string filters; array filters; filter chaining; complex filters. Custom logic.           |
| **[[6.3 Shortcode Basics]]**     | Universal shortcodes; paired shortcodes; async shortcodes; shortcode parameters; shortcode templates. Template macros.   |
| **[[6.4 Custom Shortcodes]]**    | Building shortcodes; image shortcodes; embed shortcodes; component shortcodes; shortcode libraries. Reusable components. |
| **[[6.5 Transforms]]**           | Output transforms; HTML transforms; minification; post-processing; transform timing. Build-time processing.              |
| **[[6.6 Linters & Validators]]** | HTML validation; link checking; accessibility checking; custom validators. Quality assurance.                            |
| **[[6.7 Data Filters]]**         | Filtering collections; date filters; sorting filters; grouping filters; custom logic. Data manipulation.                 |
| **[[6.8 Template Helpers]]**     | Helper functions; utility functions; computed helpers; date helpers; string helpers. Template utilities.                 |

### **[[7 Performance Optimization]]**

Master optimizing 11ty sites for maximum performance. Learn build optimization, asset optimization, caching strategies, and performance monitoring. Build sites that score perfect Lighthouse scores. Performance is 11ty's superpower—learn to leverage it fully.

| Topic                               | Focus & Purpose                                                                                                    |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **[[7.1 Build Performance]]**       | Fast builds; incremental builds; watch mode optimization; build profiling; bottleneck identification. Build speed. |
| **[[7.2 Asset Optimization]]**      | Image optimization; CSS minification; JS minification; font optimization; asset pipeline. Asset performance.       |
| **[[7.3 Caching Strategies]]**      | Data caching; fetch caching; incremental builds; cache invalidation; build caching. Smart caching.                 |
| **[[7.4 Critical CSS]]**            | Inline critical CSS; above-the-fold CSS; CSS splitting; critical extraction. First paint optimization.             |
| **[[7.5 Lazy Loading]]**            | Image lazy loading; iframe lazy loading; loading attribute; intersection observer. Deferred loading.               |
| **[[7.6 Output Optimization]]**     | HTML minification; removing whitespace; optimizing output; compression. Clean output.                              |
| **[[7.7 Performance Monitoring]]**  | Lighthouse scores; SpeedCurve; WebPageTest; performance budgets; monitoring. Tracking performance.                 |
| **[[7.8 Progressive Enhancement]]** | No-JS baseline; JavaScript enhancement; graceful degradation; accessibility-first. Resilient sites.                |

### **[[8 Headless CMS Integration]]**

Master integrating headless CMS platforms with 11ty. Learn API-driven content, GraphQL, REST APIs, and webhook deployments. Build sites that combine 11ty's speed with powerful content management. Headless CMS integration enables non-technical content editors while maintaining static site benefits.

| Topic                           | Focus & Purpose                                                                             |
| ------------------------------- | ------------------------------------------------------------------------------------------- |
| **[[8.1 Headless CMS Basics]]** | Git-based vs API-driven; CMS options; choosing a CMS; CMS comparison. Content management.   |
| **[[8.2 Git-Based CMSes]]**     | Netlify CMS; Forestry; Decap CMS; TinaCMS; git workflow; markdown editing. File-based CMS.  |
| **[[8.3 API-Driven CMSes]]**    | Contentful; Sanity; DatoCMS; Strapi; Prismic; API integration. Cloud CMS.                   |
| **[[8.4 Fetching CMS Data]]**   | Data files; async fetch; GraphQL queries; REST requests; authentication. Getting content.   |
| **[[8.5 GraphQL Integration]]** | GraphQL basics; queries; fragments; pagination; GraphQL clients. Querying APIs.             |
| **[[8.6 Content Modeling]]**    | Content types; field types; relationships; references; structured content. Data modeling.   |
| **[[8.7 Webhook Deployments]]** | Deploy hooks; automatic builds; webhook setup; build triggers; CI/CD. Automated publishing. |
| **[[8.8 Live Preview]]**        | Preview environments; draft content; preview modes; serverless preview. Content preview.    |

### **[[9 Styling & Frontend Integration]]**

Master integrating CSS frameworks, build tools, and frontend technologies with 11ty. Learn Sass, PostCSS, Tailwind, Alpine.js, and modern frontend workflows. Build complete frontend applications. 11ty works seamlessly with modern frontend tooling.

| Topic                             | Focus & Purpose                                                                                              |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **[[9.1 CSS Integration]]**       | CSS processing; CSS imports; postcss; autoprefixer; CSS organization. Styling setup.                         |
| **[[9.2 Sass/SCSS]]**             | Sass integration; Sass plugins; Sass compilation; Sass organization; Sass best practices. CSS preprocessing. |
| **[[9.3 PostCSS]]**               | PostCSS plugins; cssnano; autoprefixer; PostCSS config; modern CSS. CSS transformation.                      |
| **[[9.4 Tailwind CSS]]**          | Tailwind integration; JIT mode; PurgeCSS; Tailwind config; utility classes. Utility-first CSS.               |
| **[[9.5 JavaScript Bundling]]**   | Webpack; Rollup; esbuild; JS bundling; module bundling; code splitting. JS processing.                       |
| **[[9.6 Alpine.js Integration]]** | Alpine basics; reactive components; interactive elements; progressive enhancement. Lightweight JS.           |
| **[[9.7 Vite Plugin]]**           | 11ty + Vite; HMR; fast dev server; Vite config; modern tooling. Development experience.                      |
| **[[9.8 Design Systems]]**        | Component libraries; pattern libraries; style guides; design tokens. Systematic design.                      |

### **[[10 Deployment & Hosting]]**

Master deploying 11ty sites to production. Learn Netlify, Vercel, Cloudflare Pages, GitHub Pages, and other hosting platforms. Understand CI/CD, custom domains, and production configurations. Deployment is where your site goes live—master modern deployment workflows.

| Topic                           | Focus & Purpose                                                                                    |
| ------------------------------- | -------------------------------------------------------------------------------------------------- |
| **[[10.1 Deployment Basics]]**  | Build output; static hosting; deployment workflow; environment variables. Going live.              |
| **[[10.2 Netlify Deployment]]** | Netlify setup; netlify.toml; build settings; deploy contexts; branch deploys. Netlify platform.    |
| **[[10.3 Vercel Deployment]]**  | Vercel setup; vercel.json; build configuration; preview deployments. Vercel platform.              |
| **[[10.4 Cloudflare Pages]]**   | Cloudflare setup; pages configuration; edge functions; CF analytics. Cloudflare platform.          |
| **[[10.5 GitHub Pages]]**       | GitHub Actions; gh-pages deployment; custom domain; deployment workflow. GitHub hosting.           |
| **[[10.6 Custom Domains]]**     | DNS configuration; SSL certificates; domain verification; domain routing. Domain setup.            |
| **[[10.7 CI/CD Pipelines]]**    | Automated deployment; GitHub Actions; GitLab CI; testing in CI; deployment automation. Automation. |
| **[[10.8 Edge Functions]]**     | Serverless functions; dynamic routes; API routes; edge computing. Dynamic capabilities.            |

### **[[11 Advanced Patterns]]**

Master advanced 11ty techniques and patterns. Learn edge cases, complex configurations, and sophisticated architectures. Build large-scale sites, multi-language sites, and complex applications. Advanced patterns enable building anything with 11ty.

| Topic                             | Focus & Purpose                                                                                         |
| --------------------------------- | ------------------------------------------------------------------------------------------------------- |
| **[[11.1 Multi-Language Sites]]** | i18n strategies; locale routing; translated content; language switching; hreflang. International sites. |
| **[[11.2 Large-Scale Sites]]**    | Scaling strategies; build optimization; content organization; architectural patterns. Enterprise sites. |
| **[[11.3 Incremental Adoption]]** | Migrating to 11ty; partial conversion; hybrid approaches; gradual migration. Transitioning.             |
| **[[11.4 Custom Engines]]**       | Template engine plugins; custom parsing; extending engines; engine configuration. Engine customization. |
| **[[11.5 Serverless 11ty]]**      | On-demand builders; serverless rendering; preview modes; dynamic content. Hybrid static/dynamic.        |
| **[[11.6 Build Events]]**         | Before/after events; event listeners; build hooks; custom processing. Build lifecycle.                  |
| **[[11.7 Testing]]**              | Testing static output; accessibility testing; link checking; visual regression. Quality assurance.      |
| **[[11.8 Documentation Sites]]**  | Docs structure; search; versioning; navigation; best practices. Technical documentation.                |

### **[[12. Real-World Projects]]**

Master building production 11ty sites across use cases. Learn portfolio sites, blogs, documentation, e-commerce, and complex applications. Build complete, deployed projects. Real projects solidify understanding and provide portfolio pieces.

| Topic                               | Focus & Purpose                                                                                   |
| ----------------------------------- | ------------------------------------------------------------------------------------------------- |
| **[[12.1 Portfolio Website]]**      | Portfolio structure; project pages; about page; contact form; resume page. Personal branding.     |
| **[[12.2 Blog Platform]]**          | Blog architecture; post system; categories; tags; RSS; comments integration. Content publishing.  |
| **[[12.3 Documentation Site]]**     | Docs organization; search; versions; sidebar navigation; code examples. Technical docs.           |
| **[[12.4 Marketing Site]]**         | Landing pages; lead capture; analytics; forms; CTA optimization. Business site.                   |
| **[[12.5 E-commerce Integration]]** | Product catalog; Shopify integration; Snipcart; payment integration; shopping cart. Online store. |
| **[[12.6 Podcast Site]]**           | Episode pages; audio players; RSS podcast feed; iTunes integration; show notes. Podcast platform. |
| **[[12.7 Community Site]]**         | Event pages; member directory; resources; forum integration. Community platform.                  |
| **[[12.8 JAMstack Application]]**   | API integration; authentication; dynamic features; serverless functions. Full applications.       |

---
