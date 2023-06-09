# Notes: [Shay Howe Lesson on HTML](https://learn.shayhowe.com/html-css/building-your-first-web-page/)
#

## Terms:
  
### Elements
- Definition: 
  - Designators that define ***structure*** and ***content*** of objects within a page. 

- Use/Behavior: 
  - Headings
  - Paragraphs

- Example Syntax: 
  - `<h1>` (heading)
  - `<p>` (paragraph)

### Tags 
  - Definition: 
    - Created when `< >` surround an element. 
  
  - Use/Behavior: 
    - Opening tag marks beginning of an element. 
      - `<div>`
    - Closing tag marks end of element. 
      - `</div>`
    - Content falling between the tags is ***content*** of that element. 
      - Example: 
        - Anchor link element will have opening tag `<a>` and closing tag `</a>`
          - What falls between the two tags is the ***content*** of the anchor link. 

### Attributes
  - Definition: 
    - Properties used to provide additional information about an element. 
    - Defined within the opening tag, after an elements name. 
      - Generally have a name and a value. 
        - ex: `href="http://google.com/"`
  
  - Most commonly used: 
    - `id`    : identifies an element
    - `class` : classifies an element
    - `src`   : specifies a source for embeddable content
    - `href`  : provides hyperlink reference to linked resource

Syntax
```html
<a href="http://google.com/">Google</a>
```

  - `<` opens opening tag.
  - `a` element name (anchor in this case)
  - `href` attribute name
  - `"http://google.com/"` attribute content
  - `>` closes opening tag. 
    - (*attribute contained in opening tag of anchor element*)
  - `Google` display text for the link 
  - `</a>` closing tag
