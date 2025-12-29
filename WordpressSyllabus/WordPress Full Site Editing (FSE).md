## FSE Overview

### Interview Learning Goals

Explain what Full Site Editing is and why it fundamentally changes modern WordPress theming.

### Key Concepts

FSE (Full Site Editing) is WordPress's modern theming system introduced in WordPress 5.9 that extends the block editor (Gutenberg) from just content editing to entire site building. It represents a paradigm shift from PHP-based templates to block-based, visual site construction.

**Core Evolution:**

- **Classic Editor** (pre-2018): Simple TinyMCE text editor
- **Gutenberg/Block Editor** (2018): Block-based content creation
- **FSE** (2021+): Block-based entire site design

### Technical Details

**What Changed:**

```
Classic Theme Structure:          Block Theme Structure:
├── header.php                    ├── theme.json (central config)
├── footer.php                    ├── templates/
├── index.php                     │   ├── index.html
├── single.php                    │   ├── single.html
├── functions.php                 │   └── page.html
└── style.css                     ├── parts/
                                  │   ├── header.html
                                  │   └── footer.html
                                  ├── patterns/
                                  └── functions.php (optional)
```

### Interview Talking Points

- FSE democratizes WordPress development - non-developers can build complex sites
- Represents WordPress's future direction (default themes are FSE since Twenty Twenty-Two)
- Reduces dependency on page builders (Elementor, Divi) and custom code
- Performance benefits: 40-60% faster than page builder themes
- WYSIWYG experience - what you see in editor matches frontend

**One-liner:** "FSE is the modern WordPress theming system that builds the entire site using blocks, replacing PHP templates with visual, block-based components."

---

## What is Full Site Editing

### Interview Learning Goals

Define FSE precisely and contrast it with classic theming approaches.

### Core Definition

FSE is a comprehensive feature set that allows users to edit every aspect of their website—headers, footers, templates, and content—using the block editor from a single unified interface.

### Key Technical Details

**Access FSE:**

```php
// Navigate to: Appearance → Editor
// Or programmatically check:
if ( wp_is_block_theme() ) {
    // Site supports FSE
}
```

**What's Included in FSE:**

1. **Site Editor** - Central editing interface
2. **Global Styles** - Site-wide design system
3. **Block Themes** - Template structure using blocks
4. **Template Editor** - Visual template editing
5. **Navigation Block** - Menu system

### Classic vs FSE Comparison

|Feature|Classic Themes|FSE/Block Themes|
|---|---|---|
|Templates|PHP files|HTML/Block markup|
|Customization|Customizer UI|Site Editor|
|Menus|Menus screen|Navigation block|
|Structure|header.php, footer.php|Template parts|
|Styling|CSS files|theme.json + CSS|
|User Control|Limited|Full visual control|

### Code Example

**Classic Theme Header:**

```php
// header.php
<!DOCTYPE html>
<html <?php language_attributes(); ?>>
<head>
    <?php wp_head(); ?>
</head>
<body <?php body_class(); ?>>
    <header>
        <h1><?php bloginfo('name'); ?></h1>
        <?php wp_nav_menu(); ?>
    </header>
```

**FSE Header (parts/header.html):**

```html
<!-- wp:group {"layout":{"type":"constrained"}} -->
<div class="wp-block-group">
    <!-- wp:site-title /-->
    <!-- wp:navigation /-->
</div>
<!-- /wp:group -->
```

### Interview Talking Points

- FSE eliminates context switching between different admin screens
- Users can directly edit headers, footers without touching code
- Real-time preview of all changes
- No more Customizer - everything in Site Editor
- Lowers barrier to entry for site customization

**One-liner:** "FSE lets users edit global site structure visually instead of coding PHP templates."

---

## Block Themes vs Classic Themes

### Interview Learning Goals

Differentiate block themes from classic themes and justify when to use each approach.

### Core Differentiation

**Block Theme Requirements:**

1. **theme.json** file (mandatory)
2. **templates/** folder with HTML files
3. **parts/** folder for template parts
4. Block-based structure

### Technical Implementation

**Minimal Block Theme Structure:**

```
my-block-theme/
├── style.css (required - theme metadata)
├── theme.json (required - FSE config)
├── templates/
│   └── index.html (required - fallback template)
├── parts/
│   ├── header.html
│   └── footer.html
└── functions.php (optional - for PHP logic)
```

**style.css Header:**

```css
/*
Theme Name: My Block Theme
Theme URI: https://example.com
Author: Your Name
Description: A modern block theme
Requires at least: 6.1
Tested up to: 6.4
Requires PHP: 7.4
Version: 1.0
License: GNU General Public License v2 or later
Text Domain: my-block-theme
*/
```

**Basic theme.json:**

```json
{
  "$schema": "https://schemas.wp.org/wp/6.4/theme.json",
  "version": 2,
  "settings": {
    "appearanceTools": true,
    "layout": {
      "contentSize": "840px",
      "wideSize": "1100px"
    }
  }
}
```

### Classic Theme Compatibility

**Hybrid Theme Approach:**

```php
// functions.php - Enable FSE features in classic theme
function my_theme_setup() {
    // Add theme.json support
    add_theme_support( 'block-templates' );
    
    // Add block template part support
    add_theme_support( 'block-template-parts' );
}
add_action( 'after_setup_theme', 'my_theme_setup' );
```

### Migration Strategy

**When to Migrate:**

- Starting new projects
- Client needs visual control
- Simplifying maintenance
- Improving performance

**When to Keep Classic:**

- Complex custom post type logic
- Heavy server-side rendering
- Existing codebase with extensive customization
- Team lacks FSE knowledge

### Compatibility Considerations

```php
// Check if block theme is active
if ( wp_is_block_theme() ) {
    // FSE-specific code
    require get_template_directory() . '/inc/fse-features.php';
} else {
    // Classic theme code
    require get_template_directory() . '/inc/classic-features.php';
}
```

### Interview Talking Points

- Block themes are mandatory for FSE - no theme.json, no FSE
- Migration is one-way - converting back is difficult
- Can create hybrid themes that support both
- Plugin compatibility needs verification
- Template hierarchy still exists but uses HTML files

**One-liner:** "Block themes rely on FSE and blocks, while classic themes rely on PHP templates."

---

## Site Editor

### Interview Learning Goals

Demonstrate comprehensive understanding of the FSE user interface and its capabilities.

### Accessing Site Editor

**Navigation:**

```
Dashboard → Appearance → Editor
Or use toolbar: Admin Bar → Edit Site
```

**Programmatic Check:**

```php
// Check if Site Editor is available
if ( current_user_can( 'edit_theme_options' ) && wp_is_block_theme() ) {
    // User can access Site Editor
}
```

### Site Editor Components

**Main Interface Areas:**

1. **Left Sidebar:**
    
    - Navigation menu
    - Styles panel
    - Pages list
    - Templates list
    - Template Parts list
2. **Canvas (Center):**
    
    - Live preview
    - Block insertion
    - Visual editing
3. **Settings Panel (Right):**
    
    - Block settings
    - Template settings
    - Global styles

### Key Features

**1. Template Management:**

```html
<!-- Creating templates/single-post.html -->
<!-- wp:template-part {"slug":"header","tagName":"header"} /-->

<!-- wp:group {"layout":{"type":"constrained"}} -->
<div class="wp-block-group">
    <!-- wp:post-title {"level":1} /-->
    <!-- wp:post-date /-->
    <!-- wp:post-content /-->
</div>
<!-- /wp:group -->

<!-- wp:template-part {"slug":"footer","tagName":"footer"} /-->
```

**2. Template Parts Management:**

- Headers, Footers, Sidebars
- Reusable across multiple templates
- Synced changes globally

**3. Global Styles:** Access via Styles icon (palette) in top toolbar

### Practical Usage

**Editing Templates:**

```
1. Site Editor → Templates
2. Select template (e.g., "Single Post")
3. Click template to edit
4. Add/modify blocks
5. Save changes
```

**Editing Template Parts:**

```
1. Site Editor → Template Parts
2. Select part (e.g., "Header")
3. Modify structure
4. Changes apply site-wide automatically
```

**Managing Styles:**

```
1. Click Styles icon (palette)
2. Browse/Edit:
   - Colors
   - Typography
   - Layout
   - Blocks (per-block styling)
3. Create Style Variations
```

### Advanced Features

**Style Variations:**

```json
// styles/variation-dark.json
{
  "version": 2,
  "title": "Dark Mode",
  "settings": {
    "color": {
      "palette": [
        {
          "slug": "base",
          "color": "#1a1a1a",
          "name": "Base"
        }
      ]
    }
  }
}
```

**Keyboard Shortcuts:**

```
Ctrl/Cmd + K : Open Command Palette
Ctrl/Cmd + Z : Undo
Ctrl/Cmd + Shift + Z : Redo
Ctrl/Cmd + Shift + D : Duplicate block
/ : Block search/insert
```

### Interview Talking Points

- Site Editor consolidates all theme customization in one place
- WYSIWYG - changes preview in real-time
- No code editor switching required
- Supports keyboard shortcuts for power users
- Template hierarchy still works (index.html is fallback)
- Can export edited templates to theme files

**One-liner:** "The Site Editor is the UI for editing templates, parts, and styles in FSE."

---

## Block-Based Templates

### Interview Learning Goals

Explain how page layouts and templates are defined in FSE using block markup.

### Template Structure

**Template Hierarchy (FSE):**

```
templates/
├── index.html (required - fallback)
├── front-page.html
├── home.html
├── single.html
├── single-{post-type}.html
├── page.html
├── page-{slug}.html
├── archive.html
├── archive-{post-type}.html
├── category.html
├── tag.html
├── author.html
├── search.html
└── 404.html
```

### Block Markup Syntax

**Basic Template Example (templates/page.html):**

```html
<!-- wp:template-part {"slug":"header","theme":"my-theme","tagName":"header"} /-->

<!-- wp:group {"tagName":"main","layout":{"type":"constrained"}} -->
<main class="wp-block-group">
    <!-- wp:post-title {"level":1} /-->
    
    <!-- wp:post-content {"layout":{"type":"constrained"}} /-->
    
    <!-- wp:post-date {"format":"F j, Y"} /-->
</main>
<!-- /wp:group -->

<!-- wp:template-part {"slug":"footer","theme":"my-theme","tagName":"footer"} /-->
```

### Understanding Block Markup

**Block Anatomy:**

```html
<!-- wp:{blockName} {jsonAttributes} -->
    Block content here
<!-- /wp:{blockName} -->

<!-- Self-closing blocks -->
<!-- wp:{blockName} {jsonAttributes} /-->
```

**Complex Block Example:**

```html
<!-- wp:columns {"align":"wide"} -->
<div class="wp-block-columns alignwide">
    <!-- wp:column {"width":"66.66%"} -->
    <div class="wp-block-column" style="flex-basis:66.66%">
        <!-- wp:heading -->
        <h2>Main Content</h2>
        <!-- /wp:heading -->
        
        <!-- wp:paragraph -->
        <p>Content goes here</p>
        <!-- /wp:paragraph -->
    </div>
    <!-- /wp:column -->
    
    <!-- wp:column {"width":"33.33%"} -->
    <div class="wp-block-column" style="flex-basis:33.33%">
        <!-- wp:heading -->
        <h3>Sidebar</h3>
        <!-- /wp:heading -->
    </div>
    <!-- /wp:column -->
</div>
<!-- /wp:columns -->
```

### Template Hierarchy Fallback

**Hierarchy Logic:**

```
Request: example.com/blog-post
↓
1. single-post-blog-post.html (specific slug)
2. single-post.html (post type)
3. single.html (single content)
4. singular.html (any singular)
5. index.html (fallback)
```

### Dynamic Content Blocks

**Post Template:**

```html
<!-- wp:post-title {"level":1} /-->

<!-- wp:group {"layout":{"type":"flex","justifyContent":"space-between"}} -->
<div class="wp-block-group">
    <!-- wp:post-date /-->
    <!-- wp:post-author {"showAvatar":true} /-->
</div>
<!-- /wp:group -->

<!-- wp:post-featured-image {"align":"wide"} /-->

<!-- wp:post-content /-->

<!-- wp:post-terms {"term":"category"} /-->
<!-- wp:post-terms {"term":"post_tag"} /-->
```

### Query Loop for Archives

**Archive Template with Loop:**

```html
<!-- wp:query {"queryId":1,"query":{"perPage":10,"pages":0}} -->
<div class="wp-block-query">
    <!-- wp:post-template -->
        <!-- wp:post-title {"isLink":true} /-->
        <!-- wp:post-excerpt /-->
        <!-- wp:post-date /-->
        <!-- wp:separator /-->
    <!-- /wp:post-template -->
    
    <!-- wp:query-pagination -->
        <!-- wp:query-pagination-previous /-->
        <!-- wp:query-pagination-numbers /-->
        <!-- wp:query-pagination-next /-->
    <!-- /wp:query-pagination -->
</div>
<!-- /wp:query -->
```

### Custom Templates

**Register Custom Template:**

```php
// functions.php
function my_theme_register_templates() {
    $templates = array(
        'page-full-width' => array(
            'title' => 'Full Width Page',
            'postTypes' => array( 'page' ),
        ),
    );
    
    foreach ( $templates as $slug => $args ) {
        register_block_template( $slug, $args );
    }
}
add_action( 'init', 'my_theme_register_templates' );
```

**Theme.json Custom Template Definition:**

```json
{
  "customTemplates": [
    {
      "name": "page-full-width",
      "title": "Full Width Page",
      "postTypes": ["page"]
    },
    {
      "name": "blank",
      "title": "Blank Canvas",
      "postTypes": ["page", "post"]
    }
  ]
}
```

### Interview Talking Points

- Templates are HTML files with block markup, not PHP
- Block comments are parsed by WordPress to render content
- Template hierarchy preserved but uses .html extensions
- Can be edited visually in Site Editor
- Patterns can be inserted into templates
- Dynamic blocks (post-title, post-content) pull actual data

**One-liner:** "FSE templates are HTML files composed of block markup, not PHP."

---

## Template Parts

### Interview Learning Goals

Describe reusable structural components and their role in FSE architecture.

### What Are Template Parts?

Template parts are reusable sections of a site that can be included across multiple templates. They're the FSE equivalent of classic theme's `get_header()` and `get_footer()`.

### Structure

**Directory Layout:**

```
parts/
├── header.html
├── footer.html
├── sidebar.html
├── post-meta.html
└── comments.html
```

### Creating Template Parts

**Basic Header (parts/header.html):**

```html
<!-- wp:group {"tagName":"header","layout":{"type":"constrained"}} -->
<header class="wp-block-group">
    <!-- wp:group {"layout":{"type":"flex","justifyContent":"space-between"}} -->
    <div class="wp-block-group">
        <!-- wp:site-logo {"width":60} /-->
        
        <!-- wp:site-title {"level":0} /-->
        
        <!-- wp:navigation {"layout":{"type":"flex","setCascadingProperties":true}} /-->
    </div>
    <!-- /wp:group -->
</header>
<!-- /wp:group -->
```

**Footer Example (parts/footer.html):**

```html
<!-- wp:group {"tagName":"footer","layout":{"type":"constrained"}} -->
<footer class="wp-block-group">
    <!-- wp:columns -->
    <div class="wp-block-columns">
        <!-- wp:column -->
        <div class="wp-block-column">
            <!-- wp:heading {"level":3} -->
            <h3>About Us</h3>
            <!-- /wp:heading -->
            
            <!-- wp:paragraph -->
            <p>Your footer content here</p>
            <!-- /wp:paragraph -->
        </div>
        <!-- /wp:column -->
        
        <!-- wp:column -->
        <div class="wp-block-column">
            <!-- wp:heading {"level":3} -->
            <h3>Quick Links</h3>
            <!-- /wp:heading -->
            
            <!-- wp:navigation {"layout":{"type":"flex","orientation":"vertical"}} /-->
        </div>
        <!-- /wp:column -->
    </div>
    <!-- /wp:columns -->
    
    <!-- wp:paragraph {"align":"center"} -->
    <p class="has-text-align-center">© 2024 Your Site</p>
    <!-- /wp:paragraph -->
</footer>
<!-- /wp:group -->
```

### Including Template Parts

**In Templates:**

```html
<!-- Basic inclusion -->
<!-- wp:template-part {"slug":"header"} /-->

<!-- With specific theme -->
<!-- wp:template-part {"slug":"header","theme":"my-theme"} /-->

<!-- With tagName attribute -->
<!-- wp:template-part {"slug":"header","tagName":"header"} /-->
```

### Registering Template Parts

**In theme.json:**

```json
{
  "version": 2,
  "templateParts": [
    {
      "name": "header",
      "title": "Header",
      "area": "header"
    },
    {
      "name": "footer",
      "title": "Footer",
      "area": "footer"
    },
    {
      "name": "sidebar",
      "title": "Sidebar",
      "area": "uncategorized"
    }
  ]
}
```

**Programmatic Registration:**

```php
// functions.php
function my_theme_register_template_parts() {
    register_block_template_part( 'sidebar', array(
        'title' => __( 'Sidebar', 'my-theme' ),
        'area'  => 'sidebar',
    ) );
}
add_action( 'init', 'my_theme_register_template_parts' );
```

### Template Part Areas

**Standard Areas:**

- `header` - Site header
- `footer` - Site footer
- `sidebar` - Sidebar content
- `uncategorized` - General purpose

**Custom Areas:**

```php
// Add custom template part area
function my_theme_custom_template_part_areas( $areas ) {
    $areas[] = array(
        'area'  => 'aside',
        'label' => __( 'Aside', 'my-theme' ),
        'description' => __( 'Content for aside sections', 'my-theme' ),
        'icon'  => 'sidebar',
    );
    return $areas;
}
add_filter( 'default_wp_template_part_areas', 'my_theme_custom_template_part_areas' );
```

### Synced vs Unsynced

**Synced Pattern (Reusable Block):**

- Changes apply globally
- One source of truth
- Used for consistent elements

**Unsynced/Standard Pattern:**

- Independent instances
- Edit per usage
- Used for starting templates

### Conditional Template Parts

**Using PHP (in template):**

```php
<?php
// In a hybrid approach (requires PHP support)
if ( is_front_page() ) {
    block_template_part( 'header-home' );
} else {
    block_template_part( 'header' );
}
?>
```

**Better: Use Separate Templates:**

```
templates/
├── front-page.html (uses header-home.html)
└── index.html (uses header.html)
```

### Interview Talking Points

- Template parts are the "include" mechanism of FSE
- Edited once, changes apply everywhere used
- Accessible via Site Editor → Template Parts
- Can have multiple variations (header, header-minimal, etc.)
- TagName attribute affects semantic HTML output
- Areas help organize and categorize parts

**One-liner:** "Template parts let you reuse headers and footers across block templates."

---

## Global Styles & theme.json

### Interview Learning Goals

Show how design systems are defined and managed in block themes through theme.json.

### Understanding theme.json

theme.json is the central configuration file that defines:

- Global design tokens (colors, fonts, spacing)
- Block-specific styles
- Editor settings
- Layout defaults

### File Structure

**Complete theme.json Example:**

```json
{
  "$schema": "https://schemas.wp.org/wp/6.4/theme.json",
  "version": 2,
  "settings": {
    "appearanceTools": true,
    "useRootPaddingAwareAlignments": true,
    "layout": {
      "contentSize": "840px",
      "wideSize": "1100px"
    },
    "color": {
      "defaultPalette": false,
      "defaultGradients": false,
      "palette": [
        {
          "slug": "primary",
          "color": "#2563eb",
          "name": "Primary"
        },
        {
          "slug": "secondary",
          "color": "#64748b",
          "name": "Secondary"
        },
        {
          "slug": "base",
          "color": "#ffffff",
          "name": "Base"
        },
        {
          "slug": "contrast",
          "color": "#0f172a",
          "name": "Contrast"
        }
      ],
      "gradients": [
        {
          "slug": "primary-gradient",
          "gradient": "linear-gradient(135deg, #2563eb 0%, #7c3aed 100%)",
          "name": "Primary Gradient"
        }
      ],
      "duotone": [
        {
          "slug": "primary-duotone",
          "colors": ["#2563eb", "#7c3aed"],
          "name": "Primary Duotone"
        }
      ]
    },
    "typography": {
      "defaultFontSizes": false,
      "fontFamilies": [
        {
          "slug": "system",
          "fontFamily": "-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif",
          "name": "System Font"
        },
        {
          "slug": "heading",
          "fontFamily": "'Inter', sans-serif",
          "name": "Heading Font"
        }
      ],
      "fontSizes": [
        {
          "slug": "small",
          "size": "0.875rem",
          "name": "Small"
        },
        {
          "slug": "medium",
          "size": "1rem",
          "name": "Medium"
        },
        {
          "slug": "large",
          "size": "1.25rem",
          "name": "Large"
        },
        {
          "slug": "x-large",
          "size": "2rem",
          "name": "Extra Large"
        }
      ]
    },
    "spacing": {
      "units": ["px", "em", "rem", "vh", "vw", "%"],
      "padding": true,
      "margin": true,
      "spacingScale": {
        "steps": 0
      },
      "spacingSizes": [
        {
          "slug": "30",
          "size": "1rem",
          "name": "1"
        },
        {
          "slug": "40",
          "size": "1.5rem",
          "name": "2"
        },
        {
          "slug": "50",
          "size": "2rem",
          "name": "3"
        }
      ]
    },
    "blocks": {
      "core/button": {
        "color": {
          "palette": [
            {
              "slug": "button-primary",
              "color": "#2563eb",
              "name": "Button Primary"
            }
          ]
        }
      },
      "core/heading": {
        "typography": {
          "fontSizes": [
            {
              "slug": "heading-1",
              "size": "2.5rem",
              "name": "H1"
            }
          ]
        }
      }
    }
  },
  "styles": {
    "color": {
      "background": "var(--wp--preset--color--base)",
      "text": "var(--wp--preset--color--contrast)"
    },
    "typography": {
      "fontSize": "var(--wp--preset--font-size--medium)",
      "lineHeight": "1.6",
      "fontFamily": "var(--wp--preset--font-family--system)"
    },
    "spacing": {
      "padding": {
        "top": "0",
        "right": "var(--wp--preset--spacing--40)",
        "bottom": "0",
        "left": "var(--wp--preset--spacing--40)"
      }
    },
    "elements": {
      "link": {
        "color": {
          "text": "var(--wp--preset--color--primary)"
        },
        ":hover": {
          "color": {
            "text": "var(--wp--preset--color--secondary)"
          }
        }
      },
      "button": {
        "color": {
          "background": "var(--wp--preset--color--primary)",
          "text": "var(--wp--preset--color--base)"
        },
        "spacing": {
          "padding": {
            "top": "0.75rem",
            "right": "1.5rem",
            "bottom": "0.75rem",
            "left": "1.5rem"
          }
        },
        ":hover": {
          "color": {
            "background": "var(--wp--preset--color--secondary)"
          }
        }
      },
      "h1": {
        "typography": {
          "fontSize": "2.5rem",
          "lineHeight": "1.2"
        }
      },
      "h2": {
        "typography": {
          "fontSize": "2rem",
          "lineHeight": "1.3"
        }
      }
    },
    "blocks": {
      "core/paragraph": {
        "typography": {
          "lineHeight": "1.7"
        }
      },
      "core/heading": {
        "typography": {
          "fontFamily": "var(--wp--preset--font-family--heading)",
          "fontWeight": "700"
        }
      },
      "core/button": {
        "border": {
          "radius": "4px"
        }
      }
    }
  }
}
```

### Settings vs Styles

**Settings Section:**

- Defines available options
- Creates CSS custom properties
- Controls editor UI options

**Styles Section:**

- Applies actual styling
- Uses settings values
- Generates output CSS

### CSS Custom Properties

**How theme.json Creates CSS Variables:**

```json
{
  "settings": {
    "color": {
      "palette": [
        {"slug": "primary", "color": "#2563eb"}
      ]
    }
  }
}
```

**Generated CSS:**

```css
:root {
  --wp--preset--color--primary: #2563eb;
}

.has-primary-color {
  color: var(--wp--preset--color--primary) !important;
}

.has-primary-background-color {
  background-color: var(--wp--preset--color--primary) !important;
}
```

### Block-Level Customization

**Per-Block Settings:**

```json
{
  "settings": {
    "blocks": {
      "core/button": {
        "color": {
          "palette": [
            {
              "slug": "button-accent",
              "color": "#dc2626",
              "name": "Button Accent"
            }
          ]
        },
        "border": {
          "radius": true
        }
      }
    }
  }
}
```

### Filtering theme.json

**Modify via PHP:**

```php
// Filter theme.json data
function my_theme_json_filter( $theme_json ) {
    $new_data = array(
        'version'  => 2,
        'settings' => array(
            'color' => array(
                'palette' => array(
                    array(
                        'slug'  => 'dynamic-color',
                        'color' => get_option( 'my_custom_color', '#000000' ),
                        'name'  => __( 'Dynamic Color', 'my-theme' ),
                    ),
                ),
            ),
        ),
    );
    return $theme_json->update_with( $new_data );
}
add_filter( 'wp_theme_json_data_theme', 'my_theme_json_filter' );
```

### Style Variations

**Creating Variations (styles/dark.json):**

```json
{
  "version": 2,
  "title": "Dark Mode",
  "settings": {
    "color": {
      "palette": [
        {
          "slug": "base",
          "color": "#0f172a",
          "name": "Base"
        },
        {
          "slug": "contrast",
          "color": "#f1f5f9",
          "name": "Contrast"
        }
      ]
    }
  },
  "styles": {
    "color": {
      "background": "var(--wp--preset--color--base)",
      "text": "var(--wp--preset--color--contrast)"
    }
  }
}
```

### User Style Overrides

Users can override theme.json values via Site Editor:

- Changes stored in database
- Take precedence over theme defaults
- Can be reset to theme defaults

**Programmatic Reset:**

```php
// Reset user styles to theme defaults
function reset_user_styles() {
    delete_theme_mod( 'wp_global_styles_' . get_stylesheet() );
}
```

### Interview Talking Points

- theme.json is mandatory for block themes
- Centralizes design system in one file
- Automatically generates CSS custom properties
- Users can override via Global Styles UI
- Supports per-block customization
- Style variations allow multiple design options
- Better performance than inline styles

**One-liner:** "theme.json controls global design tokens and styles for block themes."

---

## Patterns & Reusable Blocks

### Interview Learning Goals

Explain layout reuse mechanisms and rapid site building through patterns.

### What Are Patterns?

Block patterns are pre-designed combinations of blocks that users can insert as starting layouts. They speed up site building and ensure design consistency.

### Types of Patterns

1. **Theme Patterns** - Bundled with themes
2. **Core Patterns** - WordPress default patterns
3. **Synced Patterns** (Reusable Blocks) - Single source, global changes
4. **Directory Patterns** - From wordpress.org pattern directory

### Creating Patterns

**Pattern File Structure:**

```
patterns/
├── hero-section.php
├── pricing-table.php
├── testimonials.php
└── call-to-action.php
```

**Pattern Example (patterns/hero-section.php):**

```php
<?php
/**
 * Title: Hero Section with Background
 * Slug: my-theme/hero-section
 * Categories: featured, banner
 * Keywords: hero, banner, header
 * Block Types: core/group
 * Viewport Width: 1400
 */
?>

<!-- wp:cover {"url":"<?php echo esc_url( get_template_directory_uri() . '/assets/hero-bg.jpg' ); ?>","dimRatio":50,"overlayColor":"contrast","minHeight":600,"align":"full"} -->
<div class="wp-block-cover alignfull" style="min-height:600px">
    <span aria-hidden="true" class="wp-block-cover__background has-contrast-background-color has-background-dim"></span>
    <img class="wp-block-cover__image-background" alt="" src="<?php echo esc_url( get_template_directory_uri() . '/assets/hero-bg.jpg' ); ?>" data-object-fit="cover"/>
    
    <div class="wp-block-cover__inner-container">
        <!-- wp:group {"layout":{"type":"constrained","contentSize":"840px"}} -->
        <div class="wp-block-group">
            <!-- wp:heading {"textAlign":"center","level":1,"fontSize":"x-large"} -->
            <h1 class="has-text-align-center has-x-large-font-size">Welcome to Our Site</h1>
            <!-- /wp:heading -->
            
            <!-- wp:paragraph {"align":"center"} -->
            <p class="has-text-align-center">Create amazing experiences with our platform</p>
            <!-- /wp:paragraph -->
            
            <!-- wp:buttons {"layout":{"type":"flex","justifyContent":"center"}} -->
            <div class="wp-block-buttons">
                <!-- wp:button -->
                <div class="wp-block-button">
                    <a class="wp-block-button__link wp-element-button">Get Started</a>
                </div>
                <!-- /wp:button -->
                
                <!-- wp:button {"className":"is-style-outline"} -->
                <div class="wp-block-button is-style-outline">
                    <a class="wp-block-button__link wp-element-button">Learn More</a>
                </div>
                <!-- /wp:button -->
            </div>
            <!-- /wp:buttons -->
        </div>
        <!-- /wp:group -->
    </div>
</div>
<!-- /wp:cover -->
```

**Pricing Table Pattern:**

```php
<?php
/**
 * Title: Pricing Table - Three Columns
 * Slug: my-theme/pricing-table
 * Categories: pricing, call-to-action
 */
?>

<!-- wp:columns {"align":"wide"} -->
<div class="wp-block-columns alignwide">
    <!-- wp:column {"style":{"border":{"width":"1px","style":"solid"},"spacing":{"padding":{"top":"2rem","right":"2rem","bottom":"2rem","left":"2rem"}}}} -->
    <div class="wp-block-column" style="border-width:1px;border-style:solid;padding:2rem">
        <!-- wp:heading {"textAlign":"center","level":3} -->
        <h3 class="has-text-align-center">Basic</h3>
        <!-- /wp:heading -->
        
        <!-- wp:paragraph {"align":"center","fontSize":"x-large"} -->
        <p class="has-text-align-center has-x-large-font-size"><strong>$29</strong>/month</p>
        <!-- /wp:paragraph -->
        
        <!-- wp:list -->
        <ul>
            <li>Feature 1</li>
            <li>Feature 2</li>
            <li>Feature 3</li>
        </ul>
        <!-- /wp:list -->
        
        <!-- wp:button {"width":100} -->
        <div class="wp-block-button has-custom-width wp-block-button__width-100">
            <a class="wp-block-button__link wp-element-button">Choose Plan</a>
        </div>
        <!-- /wp:button -->
    </div>
    <!-- /wp:column -->
    
    <!-- Repeat for Pro and Enterprise columns -->
</div>
<!-- /wp:columns -->
```

### Registering Patterns

**Via PHP:**

```php
// functions.php
function my_theme_register_patterns() {
    register_block_pattern_category( 'my-theme-layouts', array(
        'label' => __( 'My Theme Layouts', 'my-theme' ),
    ) );
    
    // Pattern auto-discovered from patterns/ directory
    // Or register manually:
    register_block_pattern(
        'my-theme/call-to-action',
        array(
            'title'       => __( 'Call to Action', 'my-theme' ),
            'description' => __( 'A prominent call to action section', 'my-theme' ),
            'categories'  => array( 'my-theme-layouts', 'buttons' ),
            'keywords'    => array( 'cta', 'button', 'action' ),
            'content'     => '<!-- Block markup here -->',
        )
    );
}
add_action( 'init', 'my_theme_register_patterns' );
```

### Synced Patterns (Reusable Blocks)

**Create Synced Pattern:**

```php
// Create programmatically
function create_synced_pattern() {
    $content = '<!-- wp:paragraph --><p>This content syncs everywhere</p><!-- /wp:paragraph -->';
    
    $pattern_post = array(
        'post_type'    => 'wp_block',
        'post_status'  => 'publish',
        'post_title'   => 'My Synced Pattern',
        'post_content' => $content,
    );
    
    wp_insert_post( $pattern_post );
}
```

**Usage in Templates:**

```html
<!-- Synced pattern reference -->
<!-- wp:block {"ref":123} /-->
```

### Pattern Categories

**Default Categories:**

- `featured`
- `text`
- `query`
- `header`
- `footer`
- `call-to-action`
- `banner`
- `gallery`

**Custom Categories:**

```php
function my_theme_pattern_categories() {
    register_block_pattern_category( 'pricing', array(
        'label'       => __( 'Pricing', 'my-theme' ),
        'description' => __( 'Pricing table patterns', 'my-theme' ),
    ) );
}
add_action( 'init', 'my_theme_pattern_categories' );
```

### Using Patterns in Templates

**Insert Pattern in Template:**

```html
<!-- templates/front-page.html -->

<!-- wp:pattern {"slug":"my-theme/hero-section"} /-->

<!-- wp:group {"layout":{"type":"constrained"}} -->
<div class="wp-block-group">
    <!-- wp:pattern {"slug":"my-theme/features-grid"} /-->
    
    <!-- wp:pattern {"slug":"my-theme/pricing-table"} /-->
    
    <!-- wp:pattern {"slug":"my-theme/testimonials"} /-->
</div>
<!-- /wp:group -->
```

### Dynamic Patterns

**With PHP Logic:**

```php
<?php
/**
 * Title: Dynamic Posts Grid
 * Slug: my-theme/dynamic-posts
 */

$recent_posts = get_posts( array( 'numberposts' => 3 ) );
?>

<!-- wp:group {"layout":{"type":"constrained"}} -->
<div class="wp-block-group">
    <!-- wp:columns -->
    <div class="wp-block-columns">
        <?php foreach ( $recent_posts as $post ) : setup_postdata( $post ); ?>
        <!-- wp:column -->
        <div class="wp-block-column">
            <!-- wp:heading {"level":3} -->
            <h3><?php echo esc_html( get_the_title() ); ?></h3>
            <!-- /wp:heading -->
            
            <!-- wp:paragraph -->
            <p><?php echo esc_html( get_the_excerpt() ); ?></p>
            <!-- /wp:paragraph -->
        </div>
        <!-- /wp:column -->
        <?php endforeach; wp_reset_postdata(); ?>
    </div>
    <!-- /wp:columns -->
</div>
<!-- /wp:group -->
```

### Interview Talking Points

- Patterns accelerate development by providing ready-made layouts
- Synced patterns (reusable blocks) allow global updates
- Can be inserted via inserter or programmatically in templates
- Support dynamic content through PHP
- Categories help organize and discover patterns
- Theme patterns can showcase theme capabilities

**One-liner:** "Patterns provide prebuilt layouts to compose pages quickly in FSE."

---

## Navigation in FSE

### Interview Learning Goals

Explain how WordPress menus work in the block-based system and how they differ from classic menus.

### Navigation Block Fundamentals

The Navigation block replaces classic menus with a block-based system that stores menu structure as block content rather than in separate menu locations.

### Key Differences

|Classic Menus|Navigation Block|
|---|---|
|Menu locations in code|Navigation areas (optional)|
|Separate Menus screen|Edited in Site/Block Editor|
|Menu items database|Block markup|
|`register_nav_menus()`|Block-based configuration|
|`wp_nav_menu()`|`<!-- wp:navigation /-->`|

### Basic Navigation Usage

**Simple Navigation Block:**

```html
<!-- wp:navigation {"layout":{"type":"flex","justifyContent":"right"}} /-->
```

**With Specific Menu:**

```html
<!-- wp:navigation {"ref":123,"layout":{"type":"flex","justifyContent":"space-between"}} /-->
```

**Full Configuration:**

```html
<!-- wp:navigation {
    "textColor":"contrast",
    "backgroundColor":"base",
    "overlayMenu":"mobile",
    "overlayBackgroundColor":"primary",
    "overlayTextColor":"base",
    "layout":{"type":"flex","flexWrap":"wrap","justifyContent":"right"},
    "fontSize":"small"
} -->
<!-- /wp:navigation -->
```

### Navigation Structure

**Manual Navigation Items:**

```html
<!-- wp:navigation -->
    <!-- wp:navigation-link {"label":"Home","url":"/"} /-->
    
    <!-- wp:navigation-link {"label":"About","url":"/about"} /-->
    
    <!-- wp:navigation-submenu {"label":"Services"} -->
        <!-- wp:navigation-link {"label":"Web Design","url":"/services/web-design"} /-->
        <!-- wp:navigation-link {"label":"Development","url":"/services/development"} /-->
    <!-- /wp:navigation-submenu -->
    
    <!-- wp:navigation-link {"label":"Contact","url":"/contact"} /-->
<!-- /wp:navigation -->
```

### Navigation Areas (Optional)

**Register Navigation Area:**

```php
// functions.php
function my_theme_navigation_areas() {
    register_nav_menus( array(
        'primary' => __( 'Primary Navigation', 'my-theme' ),
        'footer'  => __( 'Footer Navigation', 'my-theme' ),
    ) );
}
add_action( 'after_setup_theme', 'my_theme_navigation_areas' );
```

**Use in Template:**

```html
<!-- Use registered location -->
<!-- wp:navigation {"navigationMenuId":"primary"} /-->
```

### Responsive Navigation

**Mobile Overlay Configuration:**

```html
<!-- wp:navigation {
    "overlayMenu":"mobile",
    "overlayBackgroundColor":"contrast",
    "overlayTextColor":"base",
    "icon":"menu",
    "hasIcon":true
} -->
<!-- /wp:navigation -->
```

### Advanced Navigation Features

**Search in Navigation:**

```html
<!-- wp:navigation -->
    <!-- wp:navigation-link {"label":"Home","url":"/"} /-->
    <!-- wp:navigation-link {"label":"Blog","url":"/blog"} /-->
    <!-- wp:search {"showLabel":false,"buttonText":"Search","buttonPosition":"button-inside"} /-->
<!-- /wp:navigation -->
```

**Social Links:**

```html
<!-- wp:navigation -->
    <!-- wp:page-list /-->
    
    <!-- wp:social-links {"size":"has-small-icon-size"} -->
    <ul class="wp-block-social-links has-small-icon-size">
        <!-- wp:social-link {"url":"https://twitter.com/username","service":"twitter"} /-->
        <!-- wp:social-link {"url":"https://facebook.com/page","service":"facebook"} /-->
    </ul>
    <!-- /wp:social-links -->
<!-- /wp:navigation -->
```

### Programmatic Navigation Creation

**Create Navigation Menu:**

```php
function create_default_navigation() {
    // Create navigation post
    $nav_post_id = wp_insert_post( array(
        'post_title'  => 'Main Navigation',
        'post_status' => 'publish',
        'post_type'   => 'wp_navigation',
        'post_content' => '
            <!-- wp:navigation-link {"label":"Home","url":"/"} /-->
            <!-- wp:navigation-link {"label":"About","url":"/about"} /-->
            <!-- wp:navigation-link {"label":"Contact","url":"/contact"} /-->
        ',
    ) );
    
    return $nav_post_id;
}
```

### Fallback Navigation

**Automatic Page List:**

```html
<!-- If no navigation configured, WordPress shows page list -->
<!-- wp:navigation {"fallbackBlock":"core/page-list"} /-->
```

**Custom Fallback:**

```php
function my_theme_navigation_fallback() {
    return '<!-- wp:navigation-link {"label":"Home","url":"/"} /-->
            <!-- wp:page-list /-->';
}
add_filter( 'block_core_navigation_render_fallback', 'my_theme_navigation_fallback' );
```

### Styling Navigation

**Via theme.json:**

```json
{
  "styles": {
    "blocks": {
      "core/navigation": {
        "typography": {
          "fontSize": "1rem"
        },
        "spacing": {
          "padding": {
            "top": "1rem",
            "bottom": "1rem"
          }
        },
        "elements": {
          "link": {
            "color": {
              "text": "var(--wp--preset--color--contrast)"
            },
            ":hover": {
              "color": {
                "text": "var(--wp--preset--color--primary)"
              }
            }
          }
        }
      }
    }
  }
}
```

**Custom CSS:**

```css
/* style.css or theme CSS */
.wp-block-navigation__responsive-container-open {
    display: flex;
    align-items: center;
}

.wp-block-navigation__submenu-icon {
    margin-left: 0.5rem;
}

.wp-block-navigation .wp-block-navigation__submenu-container {
    background-color: var(--wp--preset--color--base);
    border: 1px solid var(--wp--preset--color--contrast);
}
```

### Migrating Classic Menus

**Convert Classic Menu:**

```php
function migrate_classic_menu_to_navigation() {
    $menu = wp_get_nav_menu_object( 'Primary Menu' );
    if ( ! $menu ) return;
    
    $menu_items = wp_get_nav_menu_items( $menu->term_id );
    $blocks = '';
    
    foreach ( $menu_items as $item ) {
        $blocks .= sprintf(
            '<!-- wp:navigation-link {"label":"%s","url":"%s"} /-->',
            esc_html( $item->title ),
            esc_url( $item->url )
        );
    }
    
    wp_insert_post( array(
        'post_type'    => 'wp_navigation',
        'post_status'  => 'publish',
        'post_title'   => $menu->name,
        'post_content' => $blocks,
    ) );
}
```

### Interview Talking Points

- Navigation is now a block, not a separate system
- Stored as wp_navigation post type, not in nav_menu taxonomy
- Visual editing in Site Editor
- Automatic responsive handling with overlay
- Can include any blocks (search, social, etc.)
- Fallback to page list if no menu configured
- Migration path from classic menus available

**One-liner:** "FSE replaces classic menus with the Navigation block system."

---

## Styling & CSS Handling

### Interview Learning Goals

Describe how styling is generated, applied, and managed in FSE themes.

### Style Generation System

FSE uses a sophisticated style engine that combines multiple sources:

1. **theme.json** - Design tokens and global styles
2. **Block Supports** - Per-block styling capabilities
3. **Inline Styles** - User-applied block styles
4. **Theme CSS** - Additional custom styles

### Block Supports

**Common Block Supports:**

```php
// In block.json or register_block_type
"supports": {
    "color": {
        "text": true,
        "background": true,
        "gradients": true,
        "link": true
    },
    "typography": {
        "fontSize": true,
        "lineHeight": true,
        "fontFamily": true
    },
    "spacing": {
        "margin": true,
        "padding": true,
        "blockGap": true
    },
    "border": {
        "radius": true,
        "color": true,
        "width": true,
        "style": true
    },
    "dimensions": {
        "minHeight": true
    }
}
```

### Style Engine Output

**Generated CSS Structure:**

```css
/* From theme.json */
:root {
  --wp--preset--color--primary: #2563eb;
  --wp--preset--font-size--large: 1.25rem;
  --wp--preset--spacing--40: 1.5rem;
}

/* Global styles */
body {
  background-color: var(--wp--preset--color--base);
  color: var(--wp--preset--color--contrast);
  font-family: var(--wp--preset--font-family--system);
}

/* Block-specific styles */
.wp-block-button__link {
  background-color: var(--wp--preset--color--primary);
  color: var(--wp--preset--color--base);
}

/* User customizations (inline or generated) */
.wp-block-group.custom-class {
  padding: var(--wp--preset--spacing--50);
}
```

### Inline vs Generated Styles

**Inline Styles (User Applied):**

```html
<!-- User sets custom background in editor -->
<!-- wp:group {"style":{"color":{"background":"#f3f4f6"}}} -->
<div class="wp-block-group" style="background-color:#f3f4f6">
    <!-- Content -->
</div>
<!-- /wp:group -->
```

**Generated Class Styles:**

```html
<!-- User selects preset color -->
<!-- wp:group {"backgroundColor":"primary"} -->
<div class="wp-block-group has-primary-background-color has-background">
    <!-- Content -->
</div>
<!-- /wp:group -->
```

### Custom Block Styles

**Register Block Style Variation:**

```php
// functions.php
function my_theme_register_block_styles() {
    register_block_style(
        'core/button',
        array(
            'name'  => 'outline',
            'label' => __( 'Outline', 'my-theme' ),
        )
    );
    
    register_block_style(
        'core/group',
        array(
            'name'         => 'card',
            'label'        => __( 'Card', 'my-theme' ),
            'inline_style' => '
                .wp-block-group.is-style-card {
                    border: 1px solid #e5e7eb;
                    border-radius: 8px;
                    padding: 2rem;
                    box-shadow: 0 1px 3px rgba(0,0,0,0.1);
                }
            ',
        )
    );
}
add_action( 'init', 'my_theme_register_block_styles' );
```

**Style CSS File:**

```css
/* style.css or separate file */
.wp-block-button.is-style-outline .wp-block-button__link {
    background-color: transparent;
    border: 2px solid currentColor;
    color: var(--wp--preset--color--primary);
}

.wp-block-button.is-style-outline .wp-block-button__link:hover {
    background-color: var(--wp--preset--color--primary);
    color: var(--wp--preset--color--base);
}
```

### Enqueuing Styles

**Theme Stylesheet:**

```php
// functions.php
function my_theme_enqueue_styles() {
    // Main stylesheet
    wp_enqueue_style(
        'my-theme-style',
        get_stylesheet_uri(),
        array(),
        wp_get_theme()->get( 'Version' )
    );
    
    // Block styles
    wp_enqueue_style(
        'my-theme-blocks',
        get_template_directory_uri() . '/assets/css/blocks.css',
        array( 'my-theme-style' ),
        wp_get_theme()->get( 'Version' )
    );
}
add_action( 'wp_enqueue_scripts', 'my_theme_enqueue_styles' );
```

**Editor Styles:**

```php
function my_theme_enqueue_editor_styles() {
    add_editor_style( 'assets/css/editor-style.css' );
}
add_action( 'after_setup_theme', 'my_theme_enqueue_editor_styles' );
```

### CSS Specificity Management

**Proper Specificity Hierarchy:**

```css
/* Theme defaults (lowest specificity) */
.wp-block-heading {
    font-weight: 700;
}

/* theme.json generated (medium) */
.wp-block-heading.has-large-font-size {
    font-size: var(--wp--preset--font-size--large);
}

/* User customizations (highest, via inline or classes) */
.wp-block-heading[style*="font-size"] {
    /* Inline styles have !important internally */
}
```

**Avoid Specificity Wars:**

```css
/* Bad - too specific */
body .wp-block-group .wp-block-heading.has-text-color {
    color: #000;
}

/* Good - appropriate specificity */
.wp-block-heading.has-text-color {
    color: #000;
}

/* Better - use custom properties */
.wp-block-heading {
    color: var(--wp--custom--heading--color, inherit);
}
```

### Editor/Frontend Parity

**Ensuring Consistent Styling:**

```php
// Enqueue same styles in editor
function my_theme_editor_assets() {
    wp_enqueue_style(
        'my-theme-editor',
        get_template_directory_uri() . '/assets/css/editor.css',
        array( 'wp-edit-blocks' ),
        wp_get_theme()->get( 'Version' )
    );
}
add_action( 'enqueue_block_editor_assets', 'my_theme_editor_assets' );
```

**Editor-specific Adjustments:**

```css
/* editor.css - Match frontend but account for editor UI */
.editor-styles-wrapper .wp-block-group {
    /* Same as frontend */
}

/* Adjust for editor container */
.editor-styles-wrapper {
    padding: 2rem;
    background: #fff;
}
```

### Custom Properties

**Define Custom Properties:**

```json
{
  "settings": {
    "custom": {
      "spacing": {
        "gap": "2rem"
      },
      "typography": {
        "heading-weight": "700"
      }
    }
  }
}
```

**Use in CSS:**

```css
.wp-block-group {
    gap: var(--wp--custom--spacing--gap);
}

.wp-block-heading {
    font-weight: var(--wp--custom--typography--heading-weight);
}
```

### Performance Optimization

**Minimize Inline Styles:**

```php
// Discourage inline styles, promote classes
add_theme_support( 'disable-custom-colors' );
add_theme_support( 'disable-custom-font-sizes' );

// Provide comprehensive presets instead
// in theme.json
```

**CSS Loading Optimization:**

```php
// Load block styles only when used
function my_theme_enqueue_block_styles() {
    // Conditional loading
    if ( has_block( 'core/button' ) ) {
        wp_enqueue_style( 'button-styles', /*...*/ );
    }
}
add_action( 'wp_enqueue_scripts', 'my_theme_enqueue_block_styles' );
```

### Interview Talking Points

- Style engine combines theme.json, block supports, and inline styles
- CSS custom properties provide consistent design system
- Block styles offer variations without custom CSS
- Editor/frontend parity requires careful style management
- Specificity should be minimal for maintainability
- Performance improves with generated classes over inline styles

**One-liner:** "FSE styles are generated from block supports and theme.json via the style engine."

---

## Extending FSE with Code

### Interview Learning Goals

Show how developers can customize and extend FSE beyond the visual interface.

### PHP APIs for FSE

**Key Extension Points:**

1. Block registration and customization
2. Pattern registration
3. Template filtering
4. theme.json modification
5. Custom block creation

### Registering Custom Patterns

**Simple Pattern Registration:**

```php
// functions.php
function my_theme_register_patterns() {
    register_block_pattern(
        'my-theme/feature-grid',
        array(
            'title'       => __( 'Feature Grid', 'my-theme' ),
            'description' => __( 'A 3-column feature grid', 'my-theme' ),
            'content'     => '
                <!-- wp:columns -->
                <div class="wp-block-columns">
                    <!-- wp:column -->
                    <div class="wp-block-column">
                        <!-- wp:heading {"level":3} -->
                        <h3>Feature 1</h3>
                        <!-- /wp:heading -->
                    </div>
                    <!-- /wp:column -->
                </div>
                <!-- /wp:columns -->
            ',
            'categories'  => array( 'featured' ),
            'keywords'    => array( 'features', 'grid', 'columns' ),
        )
    );
}
add_action( 'init', 'my_theme_register_patterns' );
```

### Custom Block Styles

**Register Block Style Variations:**

```php
function my_theme_register_block_styles() {
    // Button variations
    register_block_style( 'core/button', array(
        'name'  => 'gradient-fill',
        'label' => __( 'Gradient Fill', 'my-theme' ),
    ) );
    
    // Quote variations
    register_block_style( 'core/quote', array(
        'name'  => 'fancy-quote',
        'label' => __( 'Fancy Quote', 'my-theme' ),
    ) );
    
    // Group variations
    register_block_style( 'core/group', array(
        'name'  => 'shadow-box',
        'label' => __( 'Shadow Box', 'my-theme' ),
    ) );
}
add_action( 'init', 'my_theme_register_block_styles' );
```

**Style CSS:**

```css
/* Gradient button */
.wp-block-button.is-style-gradient-fill .wp-block-button__link {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border: none;
}

/* Fancy quote */
.wp-block-quote.is-style-fancy-quote {
    border-left: 4px solid var(--wp--preset--color--primary);
    font-style: italic;
    padding-left: 2rem;
    position: relative;
}

.wp-block-quote.is-style-fancy-quote::before {
    content: '"';
    font-size: 4rem;
    position: absolute;
    left: -1rem;
    top: -1rem;
    opacity: 0.2;
}

/* Shadow box */
.wp-block-group.is-style-shadow-box {
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
    border-radius: 12px;
    padding: 2rem;
}
```

### Modifying theme.json

**Filter theme.json Data:**

```php
function my_theme_filter_theme_json( $theme_json ) {
    // Get current data
    $data = $theme_json->get_data();
    
    // Add custom color based on user setting
    $custom_color = get_option( 'my_custom_brand_color', '#2563eb' );
    
    $new_data = array(
        'version'  => 2,
        'settings' => array(
            'color' => array(
                'palette' => array(
                    array(
                        'slug'  => 'brand',
                        'color' => $custom_color,
                        'name'  => __( 'Brand Color', 'my-theme' ),
                    ),
                ),
            ),
        ),
    );
    
    return $theme_json->update_with( $new_data );
}
add_filter( 'wp_theme_json_data_theme', 'my_theme_filter_theme_json' );
```

### Custom Block Registration

**Simple Custom Block:**

```php
// blocks/custom-block/block.json
{
  "apiVersion": 2,
  "name": "my-theme/custom-block",
  "title": "Custom Block",
  "category": "widgets",
  "icon": "star-filled",
  "supports": {
    "color": {
      "background": true,
      "text": true
    },
    "spacing": {
      "padding": true,
      "margin": true
    }
  },
  "attributes": {
    "content": {
      "type": "string",
      "default": ""
    }
  }
}
```

**Register the Block:**

```php
// functions.php
function my_theme_register_blocks() {
    register_block_type( __DIR__ . '/blocks/custom-block' );
}
add_action( 'init', 'my_theme_register_blocks' );
```

**Block Render Callback:**

```php
// blocks/custom-block/render.php
function my_theme_render_custom_block( $attributes, $content ) {
    $wrapper_attributes = get_block_wrapper_attributes();
    
    return sprintf(
        '<div %1$s><p>%2$s</p></div>',
        $wrapper_attributes,
        esc_html( $attributes['content'] )
    );
}

register_block_type( 'my-theme/custom-block', array(
    'render_callback' => 'my_theme_render_custom_block',
) );
```

### Template Filtering

**Modify Template Content:**

```php
// Add content to all templates
function my_theme_filter_template( $block_template ) {
    // Add analytics script to footer
    if ( 'footer' === $block_template->slug ) {
        $analytics = '<!-- wp:html -->
            <script>/* Analytics code */</script>
        <!-- /wp:html -->';
        
        $block_template->content .= $analytics;
    }
    
    return $block_template;
}
add_filter( 'get_block_template', 'my_theme_filter_template' );
```

**Programmatic Template Creation:**

```php
function create_custom_template() {
    $template_content = '
        <!-- wp:template-part {"slug":"header"} /-->
        <!-- wp:group {"layout":{"type":"constrained"}} -->
        <div class="wp-block-group">
            <!-- wp:post-title /-->
            <!-- wp:post-content /-->
        </div>
        <!-- /wp:group -->
        <!-- wp:template-part {"slug":"footer"} /-->
    ';
    
    $template = new WP_Block_Template();
    $template->slug = 'custom-landing';
    $template->title = 'Custom Landing Page';
    $template->content = $template_content;
    $template->source = 'theme';
    $template->type = 'wp_template';
    $template->theme = get_stylesheet();
    
    return $template;
}
```

### Enqueuing Assets for Blocks

**Block-specific Scripts:**

```php
function my_theme_enqueue_block_assets() {
    // Frontend and editor
    wp_enqueue_script(
        'my-theme-blocks',
        get_template_directory_uri() . '/assets/js/blocks.js',
        array( 'wp-blocks', 'wp-element', 'wp-editor' ),
        wp_get_theme()->get( 'Version' ),
        true
    );
    
    // Editor only
    if ( is_admin() ) {
        wp_enqueue_script(
            'my-theme-editor',
            get_template_directory_uri() . '/assets/js/editor.js',
            array( 'wp-blocks', 'wp-dom-ready', 'wp-edit-post' ),
            wp_get_theme()->get( 'Version' ),
            true
        );
    }
}
add_action( 'enqueue_block_assets', 'my_theme_enqueue_block_assets' );
```

### Block Filters (JavaScript)

**Modify Block Attributes:**

```javascript
// assets/js/editor.js
wp.domReady(() => {
    // Add custom class to all buttons
    wp.hooks.addFilter(
        'blocks.registerBlockType',
        'my-theme/custom-button-class',
        (settings, name) => {
            if (name === 'core/button') {
                return {
                    ...settings,
                    attributes: {
                        ...settings.attributes,
                        customClass: {
                            type: 'string',
                            default: 'my-custom-button'
                        }
                    }
                };
            }
            return settings;
        }
    );
});
```

### PHP Fallbacks for FSE Features

**Hybrid Approach:**

```php
// Support both FSE and classic approaches
function my_theme_header() {
    if ( wp_is_block_theme() ) {
        // FSE handles header
        return;
    }
    
    // Classic theme fallback
    ?>
    <header class="site-header">
        <h1><?php bloginfo( 'name' ); ?></h1>
        <?php
        wp_nav_menu( array(
            'theme_location' => 'primary',
            'menu_class'     => 'primary-menu',
        ) );
        ?>
    </header>
    <?php
}
```

### Server-Side Rendering

**Dynamic Block with Server Rendering:**

```php
function my_theme_dynamic_posts_block( $attributes ) {
    $query = new WP_Query( array(
        'posts_per_page' => $attributes['postsToShow'] ?? 3,
        'post_type'      => 'post',
        'post_status'    => 'publish',
    ) );
    
    $wrapper_attributes = get_block_wrapper_attributes();
    
    ob_start();
    ?>
    <div <?php echo $wrapper_attributes; ?>>
        <?php if ( $query->have_posts() ) : ?>
            <?php while ( $query->have_posts() ) : $query->the_post(); ?>
                <article>
                    <h3><?php the_title(); ?></h3>
                    <?php the_excerpt(); ?>
                </article>
            <?php endwhile; ?>
        <?php endif; wp_reset_postdata(); ?>
    </div>
    <?php
    return ob_get_clean();
}

register_block_type( 'my-theme/dynamic-posts', array(
    'render_callback' => 'my_theme_dynamic_posts_block',
    'attributes' => array(
        'postsToShow' => array(
            'type' => 'number',
            'default' => 3,
        ),
    ),
) );
```

### Advanced: Block Variations

**Register Block Variation:**

```javascript
// Register a variation of the core/group block
wp.blocks.registerBlockVariation('core/group', {
    name: 'my-theme/hero-section',
    title: 'Hero Section',
    description: 'A hero section with background',
    icon: 'cover-image',
    attributes: {
        align: 'full',
        backgroundColor: 'primary',
        textColor: 'base',
        style: {
            spacing: {
                padding: {
                    top: '4rem',
                    bottom: '4rem'
                }
            }
        }
    },
    innerBlocks: [
        ['core/heading', { level: 1, placeholder: 'Hero Title...' }],
        ['core/paragraph', { placeholder: 'Hero description...' }],
        ['core/buttons']
    ],
    scope: ['inserter']
});
```

### Interview Talking Points

- FSE provides extensive PHP and JavaScript APIs
- Custom blocks integrate seamlessly with FSE
- Patterns and block styles extend user options
- theme.json can be filtered programmatically
- Server-side rendering available for dynamic content
- Hybrid approaches support gradual migration
- Block variations reduce need for custom blocks

**One-liner:** "Developers extend FSE using PHP APIs and custom blocks when needed."

---

## Backward Compatibility

### Interview Learning Goals

Address how FSE coexists with classic themes, plugins, and legacy systems.

### FSE Adoption Spectrum

**Theme Types:**

1. **Pure Block Themes** - 100% FSE, no PHP templates
2. **Hybrid Themes** - FSE with PHP fallbacks
3. **Classic Themes with Block Support** - Classic with block features
4. **Pure Classic Themes** - No FSE features

### Hybrid Theme Approach

**Supporting Both Systems:**

```php
// functions.php
function my_theme_setup() {
    // Classic theme features
    add_theme_support( 'title-tag' );
    add_theme_support( 'post-thumbnails' );
    add_theme_support( 'custom-logo' );
    
    // FSE features (if theme.json exists)
    if ( file_exists( get_template_directory() . '/theme.json' ) ) {
        add_theme_support( 'block-templates' );
        add_theme_support( 'block-template-parts' );
    }
    
    // Register classic menus as fallback
    register_nav_menus( array(
        'primary' => __( 'Primary Menu', 'my-theme' ),
    ) );
}
add_action( 'after_setup_theme', 'my_theme_setup' );
```

**Conditional Template Loading:**

```php
// header.php (classic fallback)
if ( ! function_exists( 'wp_is_block_theme' ) || ! wp_is_block_theme() ) {
    ?>
    <!DOCTYPE html>
    <html <?php language_attributes(); ?>>
    <head>
        <meta charset="<?php bloginfo( 'charset' ); ?>">
        <?php wp_head(); ?>
    </head>
    <body <?php body_class(); ?>>
    <header class="site-header">
        <?php the_custom_logo(); ?>
        <?php wp_nav_menu( array( 'theme_location' => 'primary' ) ); ?>
    </header>
    <?php
}
```

### Template Fallback Hierarchy

**FSE Template Hierarchy:**

```
User Customizations (database)
    ↓
Theme HTML Templates (templates/)
    ↓
Parent Theme Templates
    ↓
WordPress Core Templates
    ↓
Classic PHP Templates (if hybrid)
```

**Programmatic Check:**

```php
function my_theme_get_template() {
    if ( wp_is_block_theme() ) {
        // FSE will handle template
        return null;
    }
    
    // Load classic template
    get_template_part( 'template-parts/content', get_post_type() );
}
```

### Plugin Compatibility

**Checking Plugin Compatibility:**

```php
// Detect if plugin uses classic hooks
function check_plugin_compatibility() {
    if ( wp_is_block_theme() ) {
        // Some plugins may need classic hooks
        // Provide compatibility shims
        add_action( 'wp_body_open', 'my_theme_compat_body_open' );
    }
}

function my_theme_compat_body_open() {
    // Trigger classic action for plugins
    do_action( 'after_body_open' );
}
```

**Widget to Block Migration:**

```php
// Provide sidebar for legacy widget plugins
function my_theme_register_sidebar() {
    if ( ! wp_is_block_theme() ) {
        register_sidebar( array(
            'name'          => __( 'Sidebar', 'my-theme' ),
            'id'            => 'sidebar-1',
            'before_widget' => '<div class="widget">',
            'after_widget'  => '</div>',
        ) );
    }
}
add_action( 'widgets_init', 'my_theme_register_sidebar' );
```

### Classic Block (Shortcode Support)

**Using Classic Block:**

```html
<!-- Wrap shortcodes in classic block -->
<!-- wp:freeform -->
[contact-form-7 id="123"]
<!-- /wp:freeform -->
```

**Better: Convert to Proper Block:**

```php
// Wrap shortcode in custom block
function my_theme_render_form_block( $attributes ) {
    $shortcode = $attributes['shortcode'] ?? '';
    return do_shortcode( $shortcode );
}

register_block_type( 'my-theme/shortcode-wrapper', array(
    'render_callback' => 'my_theme_render_form_block',
    'attributes' => array(
        'shortcode' => array(
            'type' => 'string',
            'default' => '',
        ),
    ),
) );
```

### Disabling FSE Features Selectively

**Remove Features:**

```php
// Disable template editing (keep style editing)
function my_theme_disable_template_editor() {
    remove_theme_support( 'block-templates' );
}
add_action( 'after_setup_theme', 'my_theme_disable_template_editor', 11 );

// Remove specific editor panels
function my_theme_customize_editor( $settings ) {
    $settings['__experimentalFeatures']['blocks']['core/template-part']['lock'] = true;
    return $settings;
}
add_filter( 'block_editor_settings_all', 'my_theme_customize_editor' );
```

### Content Migration

**Classic to Block Content:**

```php
// Convert classic content to blocks (WordPress does this automatically)
// But you can trigger manually:
function migrate_post_to_blocks( $post_id ) {
    $post = get_post( $post_id );
    
    if ( ! has_blocks( $post->post_content ) ) {
        // Content is classic - will be wrapped in classic block
        // Or force conversion:
        $blocks = parse_blocks( $post->post_content );
        $new_content = serialize_blocks( $blocks );
        
        wp_update_post( array(
            'ID' => $post_id,
            'post_content' => $new_content,
        ) );
    }
}
```

### Managing User Customizations

**Export Customizations:**

```php
function export_fse_customizations() {
    // Get user customizations
    global $wpdb;
    $customizations = $wpdb->get_results(
        "SELECT * FROM {$wpdb->posts} WHERE post_type IN ('wp_template', 'wp_template_part', 'wp_navigation')"
    );
    
    return $customizations;
}
```

**Reset to Theme Defaults:**

```php
function reset_fse_to_theme_defaults() {
    global $wpdb;
    
    // Delete user customizations
    $wpdb->query(
        "DELETE FROM {$wpdb->posts} 
        WHERE post_type IN ('wp_template', 'wp_template_part')
        AND post_name NOT LIKE 'wp_%'"
    );
    
    // Clear theme mods
    remove_theme_mods();
}
```

### Classic Features in FSE

**Custom Header/Background:**

```php
// FSE doesn't use custom-header/custom-background
// But can provide similar functionality

// In theme.json
{
  "settings": {
    "custom": {
      "headerImage": ""
    }
  }
}

// Provide UI to set header image
// Apply via CSS custom property
```

### Theme Switcher Compatibility

**Graceful Degradation:**

```php
function my_theme_switch_notice() {
    if ( ! wp_is_block_theme() && get_option( 'was_block_theme' ) ) {
        ?>
        <div class="notice notice-warning">
            <p><?php _e( 'You switched from a block theme. Some customizations may not transfer.', 'my-theme' ); ?></p>
        </div>
        <?php
    }
}
add_action( 'admin_notices', 'my_theme_switch_notice' );

// Track theme type
function track_theme_type() {
    update_option( 'was_block_theme', wp_is_block_theme() );
}
add_action( 'switch_theme', 'track_theme_type' );
```

### Interview Talking Points

- FSE can coexist with classic systems through hybrid themes
- Gradual migration path available
- Plugin compatibility varies - test thoroughly
- Template fallbacks provide safety net
- Classic block wraps legacy shortcodes
- User customizations stored separately from theme
- Can disable specific FSE features while keeping others

**One-liner:** "FSE can coexist with classic approaches through hybrid themes and fallbacks."

---

## Performance Considerations

### Interview Learning Goals

Discuss performance implications of FSE and optimization strategies.

### Performance Factors

**What Affects FSE Performance:**

1. Block parsing and rendering
2. Generated CSS size
3. Number of patterns
4. Database queries
5. JavaScript dependencies
6. Template complexity

### Block Parsing Cost

**Understanding Parse Time:**

```php
// Each page load parses block markup
$content = '
    <!-- wp:group -->
    <div class="wp-block-group">
        <!-- wp:heading -->
        <h2>Title</h2>
        <!-- /wp:heading -->
    </div>
    <!-- /wp:group -->
';

// parse_blocks() is called on every render
$blocks = parse_blocks( $content );
```

**Optimization:**

```php
// Cache parsed templates
function get_cached_template( $template_slug ) {
    $cache_key = 'template_' . $template_slug;
    $cached = wp_cache_get( $cache_key, 'templates' );
    
    if ( false !== $cached ) {
        return $cached;
    }
    
    $template = get_block_template( $template_slug );
    wp_cache_set( $cache_key, $template, 'templates', HOUR_IN_SECONDS );
    
    return $template;
}
```

### CSS Generation

**CSS Size Management:**

```json
// theme.json - Be selective with presets
{
  "settings": {
    "color": {
      "palette": [
        // Keep palette small (5-10 colors)
        // Each color generates multiple classes
      ]
    },
    "typography": {
      "fontSizes": [
        // Limit to essential sizes (4-6)
      ]
    }
  }
}
```

**Generated CSS Example:**

```css
/* Each preset generates ~3-5 classes */
:root {
  --wp--preset--color--primary: #2563eb;
}
.has-primary-color { color: #2563eb !important; }
.has-primary-background-color { background-color: #2563eb !important; }
.has-primary-border-color { border-color: #2563eb !important; }

/* 10 colors × 5 classes = 50 classes */
/* 8 font sizes × 2 classes = 16 classes */
/* Adds up quickly! */
```

**Optimize CSS Output:**

```php
// Disable unused features
add_theme_support( 'disable-custom-gradients' );
add_theme_support( 'disable-custom-colors' );

// Remove default WordPress block styles if not needed
function remove_wp_block_library_css() {
    wp_dequeue_style( 'wp-block-library' );
    wp_dequeue_style( 'wp-block-library-theme' );
    wp_dequeue_style( 'wc-blocks-style' ); // If using WooCommerce
}
add_action( 'wp_enqueue_scripts', 'remove_wp_block_library_css', 100 );
```

### Database Optimization

**Template Storage:**

```php
// Templates stored as posts
// Optimize queries
function optimize_template_queries() {
    // Index custom fields
    add_action( 'init', function() {
        global $wpdb;
        $wpdb->query( "
            ALTER TABLE {$wpdb->posts} 
            ADD INDEX template_type (post_type, post_status)
        " );
    } );
}
```

**Query Reduction:**

```php
// Batch template loading
function load_templates_efficiently() {
    $templates = get_posts( array(
        'post_type' => 'wp_template',
        'posts_per_page' => -1,
        'no_found_rows' => true, // Skip count query
        'update_post_meta_cache' => false, // Skip meta
        'update_post_term_cache' => false, // Skip terms
    ) );
    
    return $templates;
}
```

### Pattern Performance

**Limit Pattern Usage:**

```php
// Too many patterns slow editor
function my_theme_register_patterns() {
    // Register only essential patterns (10-20)
    // Not 50-100
    
    register_block_pattern( 'my-theme/hero', [/*...*/] );
    // ... limit to truly useful patterns
}
```

**Lazy Load Patterns:**

```php
// Load patterns on-demand
function load_pattern_category( $category ) {
    $patterns_dir = get_template_directory() . '/patterns/' . $category;
    
    if ( is_dir( $patterns_dir ) ) {
        foreach ( glob( $patterns_dir . '/*.php' ) as $pattern_file ) {
            include $pattern_file;
        }
    }
}

// Only load when category requested
add_action( 'load_pattern_category_featured', function() {
    load_pattern_category( 'featured' );
} );
```

### JavaScript Performance

**Editor Performance:**

```javascript
// Debounce expensive operations
import { debounce } from '@wordpress/compose';

const expensiveOperation = debounce((value) => {
    // Heavy computation
}, 300);

// Memoize expensive computations
import { useMemo } from '@wordpress/element';

function MyComponent({ data }) {
    const processedData = useMemo(() => {
        return expensiveProcessing(data);
    }, [data]);
    
    return <div>{processedData}</div>;
}
```

### Template Complexity

**Simple vs Complex:**

```html
<!-- Bad: Excessive nesting -->
<!-- wp:group -->
  <!-- wp:group -->
    <!-- wp:group -->
      <!-- wp:group -->
        <div>Content buried 4 levels deep</div>
      <!-- /wp:group -->
    <!-- /wp:group -->
  <!-- /wp:group -->
<!-- /wp:group -->

<!-- Good: Flat structure -->
<!-- wp:group {"layout":{"type":"constrained"}} -->
<div class="wp-block-group">
    Content at appropriate level
</div>
<!-- /wp:group -->
```

### Caching Strategies

**Object Caching:**

```php
// Cache template parts
function get_cached_template_part( $slug ) {
    $cache_key = 'template_part_' . $slug;
    $output = wp_cache_get( $cache_key );
    
    if ( false === $output ) {
        ob_start();
        block_template_part( $slug );
        $output = ob_get_clean();
        
        wp_cache_set( $cache_key, $output, '', 3600 );
    }
    
    return $output;
}
```

**Page Caching:**

```php
// FSE pages cache well with plugins
// Ensure compatibility
function fse_cache_compatibility() {
    // Don't cache logged-in users (FSE editor access)
    if ( is_user_logged_in() ) {
        header( 'Cache-Control: no-cache, must-revalidate' );
    }
}
add_action( 'template_redirect', 'fse_cache_compatibility' );
```

### Asset Loading

**Conditional Asset Loading:**

```php
function smart_asset_loading() {
    // Only load block assets when blocks are used
    $content = get_the_content();
    
    if ( has_block( 'core/gallery', $content ) ) {
        wp_enqueue_script( 'gallery-scripts' );
    }
    
    if ( has_block( 'core/video', $content ) ) {
        wp_enqueue_script( 'video-player' );
    }
}
add_action( 'wp_enqueue_scripts', 'smart_asset_loading' );
```

### Monitoring Performance

**Benchmark FSE:**

```php
function benchmark_template_rendering() {
    $start = microtime( true );
    
    // Render template
    block_template_part( 'header' );
    
    $end = microtime( true );
    $time = ( $end - $start ) * 1000; // Convert to ms
    
    error_log( "Template render time: {$time}ms" );
}
```

**Query Monitor Integration:**

```php
// Use Query Monitor plugin to track:
// - Database queries
// - Template loads
// - Block parsing time
// - Asset loading
```

### Interview Talking Points

- FSE performance depends on efficient block markup
- CSS generation scales with number of presets
- Template caching crucial for production
- Limit patterns to prevent editor slowdown
- Flat template structures perform better than deep nesting
- Conditional asset loading reduces page weight
- Monitor performance with tools like Query Monitor

**One-liner:** "FSE performance depends on efficient block markup and generated CSS."

---

## Common Pitfalls

### Interview Learning Goals

Identify typical mistakes and how to avoid them when adopting FSE.

### Pitfall 1: Overusing Inline Styles

**Problem:**

```html
<!-- User applies many inline styles -->
<!-- wp:group {"style":{"color":{"background":"#f3f4f6"},"spacing":{"padding":{"top":"2rem","bottom":"2rem"}},"typography":{"fontSize":"1.125rem"}}} -->
<div class="wp-block-group" style="background-color:#f3f4f6;padding-top:2rem;padding-bottom:2rem;font-size:1.125rem">
    Content
</div>
<!-- /wp:group -->
```

**Issues:**

- Bloated HTML
- Hard to maintain
- Inconsistent design
- Poor performance

**Solution:**

```json
// Define in theme.json
{
  "settings": {
    "color": {
      "palette": [
        {"slug": "light-gray", "color": "#f3f4f6"}
      ]
    },
    "spacing": {
      "spacingSizes": [
        {"slug": "large", "size": "2rem"}
      ]
    }
  }
}
```

```html
<!-- Use preset classes -->
<!-- wp:group {"backgroundColor":"light-gray","style":{"spacing":{"padding":"var(--wp--preset--spacing--large)"}}} -->
<div class="wp-block-group has-light-gray-background-color">
    Content
</div>
<!-- /wp:group -->
```

### Pitfall 2: Ignoring theme.json

**Problem:**

```php
// Trying to do everything in CSS
// style.css
.wp-block-button__link {
    background-color: #2563eb;
    color: white;
    padding: 12px 24px;
}

.wp-block-heading {
    font-family: 'Inter', sans-serif;
}
```

**Issues:**

- No editor preview
- Can't use Global Styles UI
- Users can override inconsistently

**Solution:**

```json
// Use theme.json first
{
  "styles": {
    "elements": {
      "button": {
        "color": {
          "background": "#2563eb",
          "text": "#ffffff"
        },
        "spacing": {
          "padding": {
            "top": "12px",
            "right": "24px",
            "bottom": "12px",
            "left": "24px"
          }
        }
      }
    },
    "blocks": {
      "core/heading": {
        "typography": {
          "fontFamily": "'Inter', sans-serif"
        }
      }
    }
  }
}
```

### Pitfall 3: Hard-Coded Content in Patterns

**Problem:**

```php
// patterns/team-section.php
register_block_pattern( 'my-theme/team', array(
    'content' => '
        <!-- wp:heading -->
        <h2>Our Team</h2>
        <!-- /wp:heading -->
        
        <!-- wp:image {"id":123,"url":"https://mysite.com/john-smith.jpg"} -->
        <img src="https://mysite.com/john-smith.jpg" alt="John Smith"/>
        <!-- /wp:image -->
        
        <!-- wp:paragraph -->
        <p>john.smith@mysite.com</p>
        <!-- /wp:paragraph -->
    ',
) );
```

**Issues:**

- Not reusable across sites
- Hard-coded URLs break on migration
- Specific content limits pattern value

**Solution:**

```php
// Use placeholder content
register_block_pattern( 'my-theme/team', array(
    'content' => '
        <!-- wp:heading {"placeholder":"Team Section Title"} -->
        <h2></h2>
        <!-- /wp:heading -->
        
        <!-- wp:image -->
        <figure class="wp-block-image"><img alt=""/></figure>
        <!-- /wp:image -->
        
        <!-- wp:paragraph {"placeholder":"Team member email or description"} -->
        <p></p>
        <!-- /wp:paragraph -->
    ',
) );
```

### Pitfall 4: Poor Template Hierarchy Understanding

**Problem:**

```
templates/
├── index.html
├── page.html
├── about.html  // Wrong! Not part of hierarchy
├── contact.html  // Wrong!
```

**Correct Structure:**

```
templates/
├── index.html
├── front-page.html
├── page.html
├── page-about.html  // Correct: page-{slug}.html
├── single.html
├── archive.html
└── 404.html
```

**Use Custom Templates Instead:**

```json
// theme.json
{
  "customTemplates": [
    {
      "name": "template-landing",
      "title": "Landing Page",
      "postTypes": ["page"]
    }
  ]
}
```

### Pitfall 5: Editor/Frontend Style Mismatch

**Problem:**

```css
/* style.css - Frontend only */
.wp-block-button__link {
    border-radius: 8px;
}

/* Editor shows default square buttons */
/* Users confused by mismatch */
```

**Solution:**

```php
// Enqueue same styles in editor
function my_theme_editor_styles() {
    add_editor_style( 'style.css' );
    
    // Or specific editor stylesheet
    add_editor_style( 'assets/css/editor-style.css' );
}
add_action( 'after_setup_theme', 'my_theme_editor_styles' );
```

```css
/* Or better: Use theme.json */
```

### Pitfall 6: Excessive Block Nesting

**Problem:**

```html
<!-- Too many groups -->
<!-- wp:group -->
  <!-- wp:group -->
    <!-- wp:group -->
      <!-- wp:group -->
        <!-- wp:columns -->
          <!-- wp:column -->
            <!-- wp:group -->
              <p>Finally, content!</p>
            <!-- /wp:group -->
          <!-- /wp:column -->
        <!-- /wp:columns -->
      <!-- /wp:group -->
    <!-- /wp:group -->
  <!-- /wp:group -->
<!-- /wp:group -->
```

**Issues:**

- Performance impact
- Confusing to edit
- Unnecessary wrapper divs

**Solution:**

```html
<!-- Simplified structure -->
<!-- wp:group {"layout":{"type":"constrained"}} -->
  <!-- wp:columns -->
    <!-- wp:column -->
      <p>Content!</p>
    <!-- /wp:column -->
  <!-- /wp:columns -->
<!-- /wp:group -->
```

### Pitfall 7: Not Providing Fallbacks

**Problem:**

```php
// Assuming FSE always works
function my_theme_setup() {
    // Only FSE features, no fallbacks
    add_theme_support( 'block-templates' );
    // No classic menu registration
    // No widget areas
}
```

**Issues:**

- Plugins expecting classic hooks fail
- No graceful degradation
- Users locked into FSE

**Solution:**

```php
function my_theme_setup() {
    // FSE features
    add_theme_support( 'block-templates' );
    
    // Fallback for plugins
    register_nav_menus( array(
        'primary' => __( 'Primary Menu', 'my-theme' ),
    ) );
    
    // Check and provide compatibility
    if ( ! wp_is_block_theme() ) {
        register_sidebar( array(
            'name' => __( 'Sidebar', 'my-theme' ),
            'id'   => 'sidebar-1',
        ) );
    }
}
```

### Pitfall 8: Ignoring Accessibility

**Problem:**

```html
<!-- No semantic HTML -->
<!-- wp:group -->
<div class="wp-block-group">
    <!-- wp:heading -->
    <h2>Header</h2>
    <!-- /wp:heading -->
</div>
<!-- /wp:group -->
```

**Solution:**

```html
<!-- Use proper semantic tags -->
<!-- wp:group {"tagName":"header"} -->
<header class="wp-block-group">
    <!-- wp:site-title {"level":0} /-->
</header>
<!-- /wp:group -->

<!-- wp:group {"tagName":"main"} -->
<main class="wp-block-group">
    <!-- wp:post-content /-->
</main>
<!-- /wp:group -->

<!-- wp:group {"tagName":"footer"} -->
<footer class="wp-block-group">
    <!-- Content -->
</footer>
<!-- /wp:group -->
```

### Pitfall 9: Not Testing with Real Content

**Problem:**

```html
<!-- Pattern designed for short text -->
<!-- wp:columns -->
  <!-- wp:column -->
    <h3>Title</h3>
    <p>Short description</p>
  <!-- /wp:column -->
<!-- /wp:columns -->

<!-- Breaks with real content -->
<!-- "Very Long Product Title That Wraps Multiple Lines" -->
```

**Solution:**

```php
// Test with varying content lengths
// Add CSS for overflow handling
```

```css
.wp-block-column h3 {
    overflow-wrap: break-word;
    hyphens: auto;
}

.wp-block-column {
    min-width: 0; /* Prevent column overflow */
}
```

### Pitfall 10: Forgetting Mobile Responsiveness

**Problem:**

```json
// theme.json - only desktop sizes
{
  "settings": {
    "layout": {
      "contentSize": "1200px",
      "wideSize": "1400px"
    }
  }
}
```

**Solution:**

```json
{
  "settings": {
    "layout": {
      "contentSize": "min(90vw, 840px)",
      "wideSize": "min(95vw, 1100px)"
    },
    "useRootPaddingAwareAlignments": true
  },
  "styles": {
    "spacing": {
      "padding": {
        "left": "var(--wp--preset--spacing--40)",
        "right": "var(--wp--preset--spacing--40)"
      }
    }
  }
}
```

### Interview Talking Points

- Theme.json should be the primary styling method
- Avoid excessive inline styles
- Maintain template hierarchy conventions
- Ensure editor/frontend parity
- Keep block nesting shallow
- Provide fallbacks for compatibility
- Test with realistic content
- Always consider mobile responsiveness
- Use semantic HTML with tagName attribute

**One-liner:** "Misusing blocks and skipping theme.json leads to brittle FSE themes."

---

## When to Use FSE

### Interview Learning Goals

Recommend FSE adoption based on project requirements and constraints.

### Ideal FSE Use Cases

**1. Content-Heavy Sites**

```
✓ Blogs
✓ News sites
✓ Marketing sites
✓ Portfolio sites
✓ Small business sites
```

**Why FSE Works:**

- Content creators can manage layouts
- Patterns speed up page creation
- Visual editing reduces developer dependency
- Built-in responsive design

**2. Client-Managed Sites**

**Scenario:**

```
Client needs:
- Update content regularly
- Create landing pages
- Modify site appearance
- No technical knowledge

FSE provides:
- Site Editor for visual control
- Patterns for page templates
- Global Styles for brand consistency
- No code required
```

**3. Rapid Prototyping**

```php
// Build MVP quickly with patterns
// patterns/landing-hero.php
// patterns/features-grid.php
// patterns/pricing-table.php
// patterns/testimonials.php
// patterns/cta-section.php

// Assemble complete landing page in minutes
```

**4. Multi-Site Networks**

```php
// Consistent design across network
// Global theme.json
// Shared patterns
// Unified Global Styles

function network_wide_theme_json() {
    // Apply brand guidelines site-wide
    // Users customize within boundaries
}
```

### When NOT to Use FSE

**1. Complex Application Logic**

**Problem:**

```php
// Heavy backend processing
// Custom database tables
// Complex user roles/permissions
// Advanced caching strategies

// FSE adds overhead without benefit
// Classic theme with custom templates better
```

**Example:**

```php
// E-commerce with custom checkout flow
// User dashboard with complex data
// SaaS application interface
// Custom booking system

// Use classic theme + REST API
// Or headless WordPress
```

**2. Highly Custom Layouts**

**When Classic is Better:**

```php
// Pixel-perfect designs
// Complex animations
// Non-standard layouts
// Heavy JavaScript interactions

// Classic PHP templates offer more control
function custom_complex_layout() {
    // Precise HTML structure
    // Custom query logic
    // Conditional rendering
    // Performance optimization
}
```

**3. Legacy System Integration**

**Problem:**

```php
// Existing codebase with:
// - Custom post types with complex meta
// - Extensive plugin dependencies
// - Custom widget system
// - Specialized shortcodes

// FSE migration too costly
// Maintain classic theme
```

**4. Performance-Critical Sites**

**High Traffic Scenarios:**

```php
// Millions of page views
// Every millisecond matters
// Highly optimized caching
// Minimal overhead required

// Classic PHP templates
// Static site generation
// Or headless approach
```

### Hybrid Approach Scenarios

**When to Mix FSE and Classic:**

```php
// Use FSE for:
// - Marketing pages (front-end, about, contact)
// - Blog posts (standard content)
// - Simple landing pages

// Use Classic for:
// - Account dashboard
// - Checkout process
// - Admin interfaces
// - Complex post types

function hybrid_template_logic() {
    if ( is_page( 'dashboard' ) ) {
        // Load classic PHP template
        get_template_part( 'template-parts/dashboard' );
    } else {
        // Use FSE template
        // FSE handles automatically
    }
}
```

### Decision Matrix

**Choose FSE When:**

```
✓ Users need visual control
✓ Content changes frequently
✓ Standard layouts sufficient
✓ Quick turnaround needed
✓ Future WordPress direction matters
✓ Client budget limited
✓ Team knows blocks/FSE
```

**Choose Classic When:**

```
✓ Complex custom logic required
✓ Pixel-perfect designs mandatory
✓ Performance critical
✓ Heavy backend processing
✓ Extensive legacy integration
✓ Developer-controlled only
✓ Specialized functionality
```

### Evaluation Questions

**Ask Before Choosing:**

```
1. Content Management:
   Q: Who will update the site?
   FSE: Non-technical users
   Classic: Developers only

2. Layout Flexibility:
   Q: How often do layouts change?
   FSE: Frequently
   Classic: Rarely

3. Customization Needs:
   Q: How much custom code required?
   FSE: Minimal
   Classic: Extensive

4. Performance Requirements:
   Q: What's the traffic volume?
   FSE: Low to medium
   Classic: High

5. Budget & Timeline:
   Q: What's the development budget?
   FSE: Lower (faster development)
   Classic: Higher (more control)

6. Maintenance:
   Q: Who maintains the site?
   FSE: Client/non-developers
   Classic: Development team
```

### Migration Considerations

**From Classic to FSE:**

```php
// Good candidates:
// - Simple classic themes
// - Standard blog layouts
// - Limited custom functionality

// Poor candidates:
// - Heavily customized themes
// - Complex page builders
// - Extensive plugin dependencies

function assess_migration() {
    $score = 0;
    
    // Check complexity indicators
    if ( count_php_templates() < 10 ) $score++;
    if ( ! uses_page_builder() ) $score++;
    if ( minimal_custom_post_types() ) $score++;
    if ( standard_widgets_only() ) $score++;
    
    return ( $score >= 3 ) ? 'Good candidate' : 'Stay classic';
}
```

### Real-World Scenarios

**Scenario 1: Small Business Site**

```
Requirements:
- 10 pages (About, Services, Contact, etc.)
- Blog
- Owner updates content monthly
- $5,000 budget

Recommendation: FSE
Rationale:
- Patterns for quick page building
- Owner can manage via Site Editor
- Cost-effective development
- Future-proof solution
```

**Scenario 2: E-commerce Platform**

```
Requirements:
- 10,000+ products
- Custom checkout flow
- Advanced filtering
- High traffic (1M+ monthly)

Recommendation: Classic or Headless
Rationale:
- Complex custom logic
- Performance critical
- Specialized functionality
- FSE adds overhead
```

**Scenario 3: Marketing Agency Site**

```
Requirements:
- Frequent landing pages
- A/B testing
- Lead generation forms
- Design variations

Recommendation: FSE with Custom Blocks
Rationale:
- Patterns for landing pages
- Quick page creation
- Custom blocks for forms/CTAs
- Global Styles for brand consistency
```

### Future-Proofing Considerations

**WordPress Direction:**

```
✓ FSE is the future of WordPress themes
✓ Core development focused on blocks
✓ New features built for FSE first
✓ Classic themes still supported but less focus

Decision Impact:
- Choose FSE for long-term alignment
- Choose classic for specialized needs
- Consider hybrid for transition period
```

### Interview Talking Points

- FSE excels for content-heavy, visually-managed sites
- Classic themes better for complex logic and performance-critical sites
- Hybrid approach works for transition or mixed requirements
- Consider user technical ability, not just features
- Budget and timeline often favor FSE
- Evaluate using decision matrix, not assumptions
- WordPress's future is FSE, but classic remains viable

**One-liner:** "Use FSE when visual control and flexibility matter more than custom PHP logic."

---

## Role in Modern Theming

### Interview Learning Goals

Position FSE within the broader WordPress ecosystem and future development.

### WordPress Evolution

**Historical Context:**

```
2003: WordPress launched (PHP templates)
2005: Theme system introduced
2008: Theme Customizer concept
2010: Menu system added
2018: Gutenberg/Block Editor
2021: FSE introduced (WP 5.9)
2022: FSE refinement (WP 6.0+)
2024-25: FSE maturity & adoption
```

### Current State (2024-2025)

**Theme Distribution:**

```
Default WordPress Themes:
- Twenty Twenty-Two (FSE)
- Twenty Twenty-Three (FSE)
- Twenty Twenty-Four (FSE)

Market Share (approximate):
- Classic themes: ~70%
- FSE themes: ~25%
- Hybrid themes: ~5%

Trend: FSE adoption increasing
```

### WordPress Roadmap Impact

**Core Focus Areas:**

```
✓ Phase 1: Editing (Gutenberg) - Complete
✓ Phase 2: Customization (FSE) - Current
→ Phase 3: Collaboration - In Progress
→ Phase 4: Multilingual - Planned

FSE is central to WordPress's future vision
```

**Active Development:**

```php
// New FSE features added each release:
// WP 6.0: Style variations
// WP 6.1: Fluid typography
// WP 6.2: Enhanced Site Editor UI
// WP 6.3: Improved pattern management
// WP 6.4: Font library
// WP 6.5: Block hooks, performance improvements
// WP 6.6: Data views, pattern overrides
```

### Impact on Theme Development

**Skill Set Evolution:**

**Traditional Theme Development:**

```php
Required Skills:
- PHP (heavy)
- WordPress template hierarchy
- Hooks & filters
- Custom queries
- Widget system
- Shortcodes
```

**Modern FSE Development:**

```javascript
Required Skills:
- JSON (theme.json)
- Block markup syntax
- CSS (design tokens)
- JavaScript (block customization)
- PHP (lighter - for extensions)
- React (for custom blocks)
```

**Shift in Approach:**

```
From: Code-first development
To: Design-first development

From: Developer-controlled
To: User-empowered

From: File-based templates
To: Database + file templates

From: CSS files
To: theme.json + minimal CSS
```

### Market Forces

**Theme Marketplace Trends:**

```
Page Builders (Elementor, Divi, Beaver Builder):
- Market leaders pre-FSE
- FSE provides native alternative
- Impact: Less dependency on page builders

WordPress.com:
- Fully embraced FSE
- Influences WordPress.org direction
- Premium themes moving to FSE

Theme Shops:
- ThemeForest: Slow FSE adoption
- WordPress.org: Increasing FSE themes
- Premium theme shops: Cautious transition
```

**Developer Sentiment:**

```
Positive:
✓ Easier for non-developers
✓ Faster development
✓ Better user experience
✓ Future-aligned

Concerns:
✗ Less control vs classic PHP
✗ Learning curve
✗ Plugin compatibility
✗ Performance questions
✗ Enterprise adoption slow
```

### Impact on Agencies & Freelancers

**Business Model Changes:**

```
Traditional Model:
- Custom theme development (high cost)
- Ongoing developer maintenance
- Technical barrier to entry

FSE Model:
- Base theme + customization (lower cost)
- Client self-service updates
- Lower barrier to entry

Impact:
- More competition
- Need to differentiate
- Focus on strategy vs code
- Custom blocks as value-add
```

**Service Offerings Evolution:**

```php
// Old service stack
function traditional_services() {
    return [
        'Custom theme development',
        'Template modifications',
        'Widget customization',
        'Shortcode creation',
        'CSS overrides'
    ];
}

// New service stack
function fse_services() {
    return [
        'theme.json configuration',
        'Pattern library creation',
        'Custom block development',
        'Site Editor training',
        'Design system implementation',
        'Performance optimization',
        'Migration services'
    ];
}
```

### Plugin Ecosystem Impact

**Plugin Compatibility:**

```
Plugins Adapting Well:
✓ Content-focused plugins
✓ SEO tools (Yoast, Rank Math)
✓ Forms (Gravity Forms adding blocks)
✓ Analytics
✓ Security

Plugins Struggling:
✗ Page builders (overlap with FSE)
✗ Custom widgets
✗ Theme-specific plugins
✗ Complex layout tools
```

**New Plugin Opportunities:**

```php
// Block pattern marketplaces
// Custom block libraries
// FSE enhancement plugins
// Migration tools
// Training/documentation tools

// Example: Pattern library plugin
function fse_pattern_marketplace_plugin() {
    // Provide curated patterns
    // Industry-specific templates
    // Premium layouts
    // One-click import
}
```

### Corporate Adoption

**Enterprise Considerations:**

```
Adoption Factors:
- Stability & long-term support ✓
- Security & compliance ✓
- Performance at scale ⚠
- Developer availability ⚠
- Training costs ⚠

Current Status:
- Large enterprises: Cautious
- Mid-size companies: Testing
- Small businesses: Adopting
- Agencies: Mixed
```

**Enterprise Concerns:**

```php
// Governance
// - Who can edit templates?
// - How to enforce brand guidelines?
// - Version control for templates?

// Solution: Custom plugins to lock down FSE
function enterprise_fse_controls() {
    // Limit template editing by role
    // Enforce theme.json standards
    // Audit trail for changes
    // Rollback capabilities
}
```

### Educational Impact

**Learning Resources:**

```
Official:
- WordPress.org documentation
- Learn WordPress courses
- WordPress TV tutorials

Community:
- WP Engine FSE resources
- Theme developer blogs
- YouTube tutorials
- Conference talks

Gap: Enterprise/advanced FSE training limited
```

**Curriculum Changes:**

```
WordPress Development Courses:
Before: Heavy PHP focus
Now: Balanced JSON/blocks/PHP

Theme Development:
Before: template-hierarchy.php
Now: theme.json + blocks

Required Knowledge:
+ JSON configuration
+ Block markup
+ Design tokens
+ React basics
- Heavy PHP (still useful)
- Widget API
```

### Long-Term Outlook

**5-Year Projection (2025-2030):**

```
2025: FSE reaches 40% theme market share
2026: Default theme only FSE
2027: Classic themes "legacy" designation
2028: FSE becomes dominant (60%+)
2029: New features FSE-only
2030: Classic themes supported but not developed

Prediction Confidence: Medium-High
Factors: WordPress direction, market adoption, developer feedback
```

**What This Means:**

```
For Developers:
- Learn FSE now (ahead of curve)
- Maintain classic skills (70% still classic)
- Hybrid approach recommended
- Specialize in FSE = competitive advantage

For Businesses:
- New sites: Consider FSE first
- Existing sites: Evaluate migration
- Training investment: FSE basics
- Plan for long-term FSE transition

For Users:
- More control without coding
- Easier site management
- Better visual experience
- Lower maintenance costs
```

### Strategic Positioning

**How to Position Yourself:**

```
1. Become FSE Expert
   - Deep theme.json knowledge
   - Custom block creation
   - Pattern design skills
   - Performance optimization

2. Offer Migration Services
   - Classic → FSE conversion
   - Risk assessment
   - Testing & QA
   - Training

3. Create FSE Products
   - Pattern libraries
   - Custom blocks
   - FSE themes
   - Training courses

4. Specialize in Hybrid
   - Best of both worlds
   - Gradual transitions
   - Complex requirement handling
```

### Interview Talking Points

- FSE is WordPress's future-first development approach
- Core team actively developing FSE features
- Market adoption growing but gradual
- Developer skill set evolving toward design tokens and blocks
- Enterprise adoption slower but increasing
- Classic themes remain viable for specific use cases
- Early FSE expertise = competitive advantage
- WordPress trajectory clear: block-first ecosystem

**One-liner:** "FSE is the future-first approach for WordPress theme development."

---

## Quick Reference Card

### Essential Commands

```php
// Check if block theme
wp_is_block_theme()

// Register pattern
register_block_pattern( $slug, $args )

// Register block style
register_block_style( $block_name, $args )

// Register template
register_block_template( $slug, $args )

// Get template
get_block_template( $slug, $template_type )
```

### Key Files

```
theme.json          - Central configuration
style.css           - Theme metadata + base styles
templates/          - Block-based templates
  └── index.html    - Required fallback
parts/              - Reusable template parts
patterns/           - Block patterns
functions.php       - PHP customization (optional)
```

### theme.json Structure

```json
{
  "$schema": "https://schemas.wp.org/wp/6.4/theme.json",
  "version": 2,
  "settings": {
    "appearanceTools": true,
    "layout": { "contentSize": "840px" },
    "color": { "palette": [] },
    "typography": { "fontSizes": [] },
    "spacing": { "spacingSizes": [] }
  },
  "styles": {
    "color": {},
    "typography": {},
    "elements": {},
    "blocks": {}
  }
}
```

### Common Block Markup

```html
<!-- Template Part -->
<!-- wp:template-part {"slug":"header"} /-->

<!-- Post Content -->
<!-- wp:post-title /-->
<!-- wp:post-content /-->

<!-- Query Loop -->
<!-- wp:query -->
  <!-- wp:post-template -->
    <!-- Loop content -->
  <!-- /wp:post-template -->
<!-- /wp:query -->

<!-- Navigation -->
<!-- wp:navigation /-->
```

### Interview Preparation Checklist

```
☐ Understand FSE vs classic difference
☐ Know theme.json structure
☐ Explain template hierarchy
☐ Describe Site Editor capabilities
☐ Discuss performance considerations
☐ Identify common pitfalls
☐ Articulate when to use FSE
☐ Position FSE in WordPress future
☐ Practice code examples
☐ Review recent WordPress releases
```

---

## Conclusion

This comprehensive doctrine covers all major aspects of WordPress Full Site Editing from an interview perspective. Each section includes:

- **Learning goals** for what to communicate
- **Technical details** with code examples
- **Practical applications** and real-world scenarios
- **Interview talking points** for concise answers
- **One-liners** for quick recall

**Study Approach:**

1. Read through each section thoroughly
2. Practice explaining concepts aloud
3. Write code examples from memory
4. Review one-liners daily
5. Connect concepts across sections
6. Stay updated with latest WordPress releases

**Key Takeaways:**

- FSE is WordPress's future direction
- theme.json is central to FSE architecture
- Visual editing empowers non-developers
- Performance requires thoughtful implementation
- Classic themes remain viable for specific use cases
- Hybrid approaches ease transition
- Continuous learning essential as FSE evolves

Good luck with your interview! 🚀