# Filip Hric Slidev theme

Local theme matching the editorial design in the `filiphric.com-new` project: warm paper, Archivo headings, Instrument Serif emphasis, IBM Plex Mono labels, and a Silkscreen wordmark. Colors come from `assets/css/editorial/colors.css`; type choices and weights come from `typography.css` and `editorial.css`.

Use `theme: ./theme` in the deck's headmatter. The theme uses light mode and bundles its fonts locally.

Layouts: `cover` (first slide), `default` (content), `section` (chapter divider), and `media` (full-size video, without a footer). Use italic Markdown inside a heading for the site's serif voice, or `<mark>` for a yellow highlight. Add `class: compact` in a slide's frontmatter for tighter spacing between subheadings and paragraphs.

Adjust shared colors and typography in `styles/theme.css`. Font files and their upstream licenses are in `fonts/`.

For a heading and short explanation beside an image, use `layout: illustration`. Put the heading and text in the default slot, then add `::image::` followed by the image Markdown.
