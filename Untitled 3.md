
### **1.1 WordPress Development Foundations**

Master modern WordPress setup and essential development skills. Learn local development, version control, WordPress architecture, and professional workflows. Think production-ready—not amateur setups, but professional environments used in agencies and companies. This section establishes the foundation for all WordPress development. Jobs expect modern tooling; basic XAMPP knowledge is insufficient.

| Topic                                      | Focus & Purpose                                                                                                                                                                        | Portfolio Project                                                                                                              |
| ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **[[1.1.1 Professional Dev Environment]]** | Local by Flywheel or DevKinsta setup; WordPress structure; database management; multiple sites; staging workflows; WP-CLI basics; debugging tools; professional environment standards. | **Project:** Set up local dev environment with 3 WordPress installations; document setup process; create deployment checklist. |
| **[[1.1.2 Git & Version Control]]**        | Git basics; .gitignore for WordPress; branching; committing; GitHub/Bitbucket; deployment workflows; team collaboration; Git for WordPress best practices.                             | **Project:** Initialize Git repo for WordPress site; create proper .gitignore; make 10+ meaningful commits; push to GitHub.    |
| **[[1.1.3 WordPress Architecture]]**       | Core file structure; wp-content folder; database tables; template hierarchy; the Loop; hooks system (actions/filters); query system; constants; understanding WordPress internals.     | **Project:** Diagram WordPress request lifecycle; identify key hooks; document template hierarchy for your theme.              |
| **[[1.1.4 PHP for WordPress]]**            | PHP 8+ essentials; WordPress coding standards; namespaces; Composer basics; object-oriented PHP; modern PHP patterns; code quality tools (PHPCS).                                      | **Project:** Write WordPress plugin using OOP, namespaces, and WPCS standards; pass Code Sniffer validation.                   |

### **1.2 Block Theme Development (Modern Standard)**

Master block-based theme development using Full Site Editing—the primary approach for new WordPress themes in 2025. Learn theme.json, template parts, block patterns, and Site Editor. Block themes are the future of WordPress; this is the #1 skill employers want. Essential for modern WordPress jobs.

|Topic|Focus & Purpose|Portfolio Project|
|---|---|---|
|**[[1.2.1 Block Theme Fundamentals]]**|FSE overview; theme.json structure; HTML templates; template parts (header, footer); minimal functions.php; block theme requirements; style.css; Site Editor.|**Project:** Create complete block theme from scratch with theme.json; 5+ templates; 3+ template parts; deploy live.|
|**[[1.2.2 theme.json Mastery]]**|Settings configuration; color palettes; typography system; layout settings; spacing scale; custom settings; style variations; version 2 vs 3 features.|**Project:** Build comprehensive theme.json with custom color palette, type scale, spacing system; create 2 style variations.|
|**[[1.2.3 Block Patterns & Templates]]**|Creating block patterns; pattern categories; reusable layouts; template organization; pattern libraries; synced patterns; pattern best practices.|**Project:** Create 10+ custom block patterns (hero, CTA, testimonials, team, pricing); organize in categories.|
|**[[1.2.4 Full Site Editing]]**|Site Editor workflows; editing templates live; global styles; navigation blocks; template editing; preview modes; exporting changes.|**Project:** Complete website using only Site Editor; document workflow; create video tutorial of editing process.|

### **1.3 Classic Theme Development & PHP**

Master traditional PHP-based theme development essential for maintaining existing sites and hybrid approaches. Learn template files, WordPress hooks, custom post types, and core WordPress functions. Classic themes power 70%+ of existing sites—this knowledge is critical for agency work and freelancing.

|Topic|Focus & Purpose|Portfolio Project|
|---|---|---|
|**[[1.3.1 Theme Structure & Templates]]**|Required files; template hierarchy; template tags; the Loop; WP_Query; custom queries; template files (index, single, page, archive, 404); get_header/footer/sidebar.|**Project:** Convert static HTML template to WordPress theme; implement all template files; proper hierarchy.|
|**[[1.3.2 Hooks & Functions]]**|Actions vs filters; add_action/add_filter; hook priorities; common hooks; functions.php organization; theme setup; add_theme_support; creating custom hooks.|**Project:** Build functions.php with 20+ hooks; custom functionality; proper organization; documented code.|
|**[[1.3.3 Custom Post Types & Taxonomies]]**|register_post_type(); post type arguments; custom taxonomies; register_taxonomy(); archive templates; single templates; query modifications.|**Project:** Create portfolio post type with categories/tags; custom fields; archive page; single template.|
|**[[1.3.4 Advanced Template Features]]**|Custom fields; metaboxes; widget areas; navigation menus; wp_nav_menu(); post thumbnails; image sizes; child themes; theme customization.|**Project:** Add metaboxes, custom widgets, 3 menu locations, 4 widget areas; implement featured images.|

### **1.4 Custom Block Development & JavaScript**

Master creating custom Gutenberg blocks—the most in-demand WordPress skill in 2025. Learn React basics, block development, and modern JavaScript. Custom blocks extend WordPress capabilities and are required for advanced client projects. Essential for mid-level+ positions.

|Topic|Focus & Purpose|Portfolio Project|
|---|---|---|
|**[[1.4.1 Block Development Basics]]**|@wordpress/create-block; block.json; registerBlockType(); block attributes; edit and save functions; InspectorControls; block structure; development workflow.|**Project:** Create 3 custom blocks: testimonial slider, pricing table, team member grid; publish to portfolio.|
|**[[1.4.2 React for WordPress]]**|React fundamentals; JSX; components; props; state; hooks (useState, useEffect); WordPress components library; @wordpress packages.|**Project:** Build interactive block using React state; real-time preview; multiple controls; advanced functionality.|
|**[[1.4.3 Block Editor Components]]**|RichText; MediaUpload; InnerBlocks; BlockControls; color controls; common components; styling blocks; editor vs frontend styles.|**Project:** Create content-rich block using 5+ WordPress components; proper styling; responsive design.|
|**[[1.4.4 Dynamic & Advanced Blocks]]**|Server-side rendering; render_callback; dynamic data; ACF Blocks; block patterns; block variations; advanced block features.|**Project:** Build dynamic block pulling from custom post type; ACF integration; create block variations.|

### **1.5 WooCommerce Development**

Master WooCommerce theme development—essential for e-commerce projects that make up 40% of WordPress work. Learn shop templates, product display, checkout customization, and WooCommerce hooks. E-commerce skills significantly increase your hourly rate and job opportunities.

|Topic|Focus & Purpose|Portfolio Project|
|---|---|---|
|**[[1.5.1 WooCommerce Templates & Hooks]]**|Template structure; overriding templates; product loop; single product; cart/checkout; WooCommerce hooks; customization patterns; shop page optimization.|**Project:** Create custom WooCommerce theme; override 10+ templates; customize product display; optimize checkout.|
|**[[1.5.2 Product Display & Features]]**|Product grids; filters; sorting; custom product types; product variations; gallery customization; related products; upsells; cross-sells.|**Project:** Build custom product archive with filters, ajax loading; custom single product layout; related products.|
|**[[1.5.3 Cart, Checkout & Performance]]**|Cart customization; checkout fields; payment gateway display; order process; WooCommerce optimization; large catalog handling; caching strategies.|**Project:** Optimize WooCommerce site to 90+ PageSpeed; custom checkout process; add custom fields.|

### **1.6 Performance, Security & SEO**

Master creating fast, secure, SEO-optimized WordPress sites. Learn Core Web Vitals optimization, security best practices, and technical SEO implementation. Performance and security are non-negotiable for professional work—slow, insecure sites lose clients and traffic.

|Topic|Focus & Purpose|Portfolio Project|
|---|---|---|
|**[[1.6.1 Core Web Vitals & Performance]]**|LCP, INP, CLS optimization; image optimization; WebP/AVIF; lazy loading; critical CSS; minification; caching strategies; CDN integration; database optimization.|**Project:** Take 50-score site to 90+ on PageSpeed Insights; document optimizations; before/after metrics.|
|**[[1.6.2 WordPress Security]]**|Data validation; sanitization; escaping output; nonces; SQL injection prevention; current_user_can(); file security; security best practices; vulnerability prevention.|**Project:** Security audit of WordPress site; fix 10+ vulnerabilities; implement security hardening; document fixes.|
|**[[1.6.3 Technical SEO & Analytics]]**|Schema markup; XML sitemaps; robots.txt; meta tags; Open Graph; structured data; Google Analytics 4 setup; Search Console integration; technical SEO checklist.|**Project:** Implement complete SEO setup; schema markup for 5+ types; verify in Search Console; GA4 tracking.|

### **1.7 Page Builders & Client Tools**

Master Elementor and popular page builders—required for 60% of WordPress jobs. Learn Elementor Pro, custom widgets, and client-friendly workflows. Page builders enable non-technical clients to manage content while you control the design system.

|Topic|Focus & Purpose|Portfolio Project|
|---|---|---|
|**[[1.7.1 Elementor Development]]**|Elementor basics; Elementor Pro; Theme Builder; custom widgets; dynamic content; templates; popup builder; WooCommerce builder; when to use Elementor.|**Project:** Create complete Elementor-based site; 5+ custom widgets; dynamic templates; client-friendly CMS.|
|**[[1.7.2 Advanced Page Builders]]**|WPBakery basics; Divi overview; Beaver Builder; builder comparison; custom modules; theme integration; performance considerations; builder best practices.|**Project:** Build comparable layouts in 2 different builders; document pros/cons; create client guide.|
|**[[1.7.3 Client Handoff & Training]]**|Documentation; video tutorials; client training; content management guides; WordPress basics for clients; support strategies; maintenance plans.|**Project:** Create complete client handoff package: documentation, video tutorials, maintenance plan, support guide.|

### **1.8 Modern WordPress & Headless**

Master headless WordPress and modern architectures. Learn REST API, GraphQL, Next.js integration, and decoupled WordPress. Headless WordPress is growing rapidly for performance-critical projects and opens doors to high-paying opportunities.

|Topic|Focus & Purpose|Portfolio Project|
|---|---|---|
|**[[1.8.1 REST API & GraphQL]]**|WP REST API; custom endpoints; authentication; WPGraphQL; queries; mutations; REST vs GraphQL; API security; when to use APIs.|**Project:** Create custom REST API endpoint; build WPGraphQL schema; document API; create Postman collection.|
|**[[1.8.2 Headless WordPress]]**|Headless architecture; Next.js + WordPress; Static Site Generation; Server-Side Rendering; headless benefits; deployment; when to go headless.|**Project:** Build headless WordPress site with Next.js; static generation; deploy to Vercel; document setup.|
|**[[1.8.3 Headless WooCommerce]]**|WooCommerce API; headless e-commerce; cart management; checkout flow; payment integration; headless WooCommerce advantages; implementation patterns.|**Project:** Create headless WooCommerce storefront; Next.js frontend; complete checkout flow; payment integration.|

### **1.9 Portfolio Development & Client Acquisition**

Master building a portfolio that gets you hired. Learn project documentation, case study creation, freelance platform optimization, and client acquisition strategies. Your portfolio is more important than your resume—this section gets you paying work.

|Topic|Focus & Purpose|Portfolio Project|
|---|---|---|
|**[[1.9.1 Portfolio Website Creation]]**|Portfolio structure; showcasing projects; case study format; live demos; GitHub integration; testimonials; contact forms; personal branding; portfolio SEO.|**Project:** Build complete portfolio website; 5+ case studies; live demos; testimonials; optimized for conversions.|
|**[[1.9.2 Case Study Documentation]]**|Before/after metrics; challenge-solution-results format; visual documentation; quantifying impact; storytelling; technical details; client testimonials; portfolio standards.|**Project:** Create 5 detailed case studies from your projects; professional photography; metrics; client quotes.|
|**[[1.9.3 Freelance Platforms]]**|Upwork profile optimization; Fiverr gigs; Codeable application; Toptal; proposal writing; portfolio presentation; pricing; platform strategies; getting first clients.|**Project:** Set up profiles on 3 platforms; write 5 gig descriptions; create proposal templates; get first review.|
|**[[1.9.4 Client Communication]]**|Requirement gathering; project scoping; expectation management; technical explanations; progress updates; conflict resolution; professional communication.|**Project:** Create communication templates: intake form, proposal, contract, progress reports, handoff docs.|

### **1.10 Professional Skills & Career Development**

Master the business skills that separate successful developers from those who struggle. Learn pricing, project management, time estimation, and professional development. Technical skills get you started—business skills make you successful and highly paid.

|Topic|Focus & Purpose|Portfolio Project|
|---|---|---|
|**[[1.10.1 Pricing & Project Scoping]]**|Hourly rates ($20-150/hr based on skill); value-based pricing; project estimation; scope documentation; contracts; payment terms; rate negotiation.|**Project:** Create pricing sheet; proposal templates; contract templates; project estimation spreadsheet.|
|**[[1.10.2 Project Management]]**|Time tracking; meeting deadlines; task management; communication schedules; managing client expectations; handling revisions; project workflows.|**Project:** Document your project management system; templates; workflows; time tracking setup; client communication schedule.|
|**[[1.10.3 WordPress Community]]**|Contributing to WordPress core; WordCamps; meetups; forums; building reputation; networking; speaking; writing; giving back; community benefits.|**Project:** Attend 2 WordPress meetups/events; contribute to forums; write blog post; submit theme/plugin to repository.|
|**[[1.10.4 Career Pathways]]**|Resume optimization; LinkedIn; GitHub showcase; job applications; interviews; salary negotiation; freelance vs agency vs in-house; career growth.|**Project:** Optimize resume and LinkedIn; apply to 10 jobs; conduct 3 informational interviews; prepare interview answers.|
