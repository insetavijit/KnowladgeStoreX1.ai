| **Subtopic** | **Focus & Purpose** | **Key Concepts / Details** | **One-Line Recall** |
| :--- | :--- | :--- | :--- |
| **2.1.4 Layout Chaining (Parent/Child)** | Hierarchical composition | `layout` front matter in a layout file; wrapping wrappers | Layouts can use layouts too. |
| **[[2.1.4.1 The Chain Concept]]** | Mental Model | Content -> Page Layout -> Base Layout; matryoshka dolls analogy | Putting a box inside a box. |
| **[[2.1.4.2 Creating a Chain]]** | Implementation | Adding `layout: base.njk` to `page.njk`; ensuring `{{ content }}` exists in all layers | Just add front matter to the layout file. |
| **[[2.1.4.3 Data Bubbling]]** | Data Flow | How variables move up the chain; `title` usage in base layout | Data travels up to the root. |
| **[[2.1.4.4 Avoiding Duplication]]** | DRY Principle | Defining HEAD/BODY in base only; child layouts focus on content structure | Don't repeat the HTML structure. |
| **[[2.1.4.5 Nesting Limits]]** | Practicality | Deep nesting complexities; performance considerations (negligible mostly); readability | Don't go too deep or you'll get lost. |
