
## Section 1: YAML Frontmatter (Data Properties)

This section, enclosed by `---`, defines the note's **metadata** as Obsidian Properties (YAML).

| **Template Line(s)**             | **Function**                                                                                                                                                                                              | **Organization Purpose**                                               |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `---`...`---`                    | **Defines the properties block.**                                                                                                                                                                         | Essential for Dataview and Obsidian search.                            |
| `citekey: {{citekey}}`           | Populates the note's unique Zotero ID.                                                                                                                                                                    | Primary key for linking and queries.                                   |
| `aliases: ...`                   | Creates a short, human-readable name for the note (e.g., `Author et al. (Year) Title`).                                                                                                                   | Makes the note easy to find via search and linking.                    |
| `title: "{{title                 | replace('"',"'")}}"`                                                                                                                                                                                      | Populates the full paper title.                                        |
| `{%- for type, creators ... %}`  | **Complex Creator Logic:** Iterates through authors/editors, groups them by type, and formats them (e.g., `authors: - FirstName LastName`).                                                               | Provides structured author data for filtering/sorting by contributor.  |
| `year: {% if date %}{{date       | format("YYYY")}}{% endif %}`                                                                                                                                                                              | Extracts the year from the date field.                                 |
| `item-type: {{itemType           | ...}}`                                                                                                                                                                                                    | Populates the document type (e.g., Journal Article, Conference Paper). |
| `publisher: ...`                 | Populates the journal/publication title or publisher name.                                                                                                                                                | Context for source quality/domain.                                     |
| `{%- if notes.length > 0 ... %}` | **Short Note Extraction:** This complex block iterates over notes taken directly in Zotero, filters them by word count (`longShortCutoff`), and lists short notes directly in the YAML `comments:` field. | Keeps quick, short mental notes accessible in the Properties block.    |
| `tags: ...`                      | Lists Zotero tags as YAML tags (`- tag1`).                                                                                                                                                                | **Crucial for topic organization and filtering.**                      |
| `doi: https://doi.org/{{DOI}}`   | Populates the Digital Object Identifier.                                                                                                                                                                  | Essential for persistent external linking.                             |
| `cssclasses: - literature-note`  | Applies a specific CSS class for styling the note.                                                                                                                                                        | Visual identification and targeted styling.                            |
| `attachments: ...`               | Lists the file paths of attached PDFs.                                                                                                                                                                    | Allows Obsidian to track the local PDF file.                           |
| `libraryID: {{libraryID}}`       | The unique Zotero library ID.                                                                                                                                                                             | Ensures data synchronization works correctly.                          |

---
## Section 2: Persisted Manual Input (Key Takeaways & Processing)

This section is where you manually add information _after_ the import. The key feature here is the `{% persist "notes" %}` block.

|**Template Line(s)**|**Function**|**Organization Purpose**|
|---|---|---|
|**`BUTTON[update-litnote]`**|Renders a button that triggers the Zotero Integration plugin to **re-import** data and highlights.|**Core function** for updating notes after adding new highlights.|
|`{% persist "notes" %}`...`{% endpersist %}`|**Persistence Block:** Tells the plugin to preserve all content between these tags upon re-import.|**Critical:** Ensures your manual `Key takeaways` and `Processing` status are _never_ overwritten.|
|`%% begin notes %%`...`%% end notes %%`|**CLUTTER/ANCHORS:** These gray lines are _generated by the plugin_ to mark the beginning and end of the persistent area.|**Unavoidable but ignorable.** Their presence confirms the persistence is working.|
|`## Key takeaways`|Your personal summary section.|**Central research function.** Where you synthesize findings in your own words.|
|`- <% tp.file.cursor(1) %>`|**Templater Cursor:** Places your cursor here immediately after note creation.|Improves workflow speed; you can start writing immediately.|
|`**Status**:: new`|A Dataview field you manually update (e.g., to `reading`, `processed`, `archive`).|**Workflow tracking:** Allows you to query notes that still need processing.|

---
## Section 3: Links and Metadata

This section presents key links and calculated fields in readable Markdown format.

|**Template Line(s)**|**Function**|**Organization Purpose**|
|---|---|---|
|`> [!info]- Info 🔗 [**Zotero**]...`|**Info Callout:** Displays links in a compact, collapsible block.|Reduces visual noise while keeping links accessible.|
|`[**Zotero**]({{desktopURI}})`|Link to open the item in the Zotero desktop app.|Quick access to the source Zotero record.|
|`[**PDF-1**](file:///{{attachment.path ...}})`|Link to open the _local_ PDF file in your default PDF reader.|**Direct access to the source document.**|
|`{% if bibliography %}`...`{% endif %}`|Populates the formatted citation (e.g., APA, Chicago) if available.|Quick copy-paste for citations in papers/essays.|
|`{% if pageCount > 0 ... %}`|**Reading Time Logic:** Calculates the approximate reading time based on page count (`readingSpeed` and `wordsPerPage`).|**Workflow management:** Helps prioritize long vs. short papers.|
|`> [!abstract]- Abstract`|**Abstract Callout:** Displays the paper's abstract.|Provides immediate context and summary without opening the PDF.|
|`> [!quote]- Citations ... \```query`|**Citations Query:** Embeds a Dataview/Datacore query to find all other notes that link to this paper using the citekey.|**Core Interlinking:** Shows the paper's influence across your vault.|

---
## Section 4: Zotero Notes and Highlights

This is the most complex section, responsible for importing and formatting your annotations (highlights and notes) taken within Zotero's PDF reader.

|**Template Line(s)**|**Function**|**Organization Purpose**|
|---|---|---|
|`{%- if longnotes.length > 0 -%}`|**Long Zotero Notes:** Loops through Zotero notes that exceeded the `longShortCutoff` (20 words, defined in your YAML).|Imports substantial, paragraph-length notes/reflections written directly in Zotero.|
|`{% persist "annotations" %}`|**Persistence Block:** Preserves the imported highlights when you re-import.|**Crucial:** Prevents highlights from being re-imported or re-ordered every time you update the note.|
|`{% set grouped_annotations ... %}`|Groups all highlights by the **color** you used in Zotero.|**Structural organization:** Groups related ideas/concepts together.|
|`{%- for color, colorValue in colorValueMap -%}`|Loops through each color group.|**Thematic Categorization:** Each color gets its own heading (e.g., **❓ Problem formulation**).|
|`### {{colorValue.heading}} %% fold %%`|Creates a Level 3 heading for the color group, which is **collapsible** in Obsidian.|Makes long highlight lists manageable and organized by theme/color.|
|`{{colorValue.symbol}} {{annotation.annotatedText ...}}`|Formats the highlighted text, prefixing it with a symbol (`@`, `$` , `&` etc.) based on the color.|**Visual signal** for the highlight's purpose (e.g., `@` for Problem, `$` for Takeaway).|
|`{{citationLink}}`|Provides a link to the specific page of the PDF where the highlight was made.|**Source verification:** Quick jump to the highlight context in the PDF.|
|`{% elif (annotation.comment ...).indexOf("todo ") !== -1 %}`|A powerful conditional that checks if the Zotero annotation comment contains the text `"todo "`.|**Actionable Research:** If you comment "todo rewrite this," it creates an **Obsidian checkbox** in the note.|

---

---

## 🎯 Purpose of the `First-page` Section

The **first page section** is part of the optional metadata extraction and is primarily used for **citation tracking** and **context setting**.

The following code block is responsible for calculating the page count and, if the `pages` field in Zotero contains a range (e.g., "10-25"), determining the starting page.

Django

```
{%- if firstPage %}
> **First-page**:: {{firstPage}}
{%- endif -%}
```

The specific purpose of tracking the first page is:

- **Context for Short Notes:** For journal articles, tracking the starting page of the article helps in quickly locating the full context within the journal issue, especially when dealing with physical copies or static PDFs where Zotero's deep linking might fail.
    
- **Citation Management:** In some citation styles (though not typically needed for in-text citations), the starting page of an article or chapter is required metadata. By having it as a field, it's readily accessible.
    
- **Reading Orientation:** It immediately tells you where the _article_ begins, which can be useful when an attached PDF includes frontmatter or covers.
    

---

## 🔍 Other Key Template Features Not Fully Covered

While we've covered the major sections (YAML, Persistence, Info, Annotations), here are other powerful features or content that haven't been fully clarified:

### 1. Zotero Note Separation (Short vs. Long)

Your template includes an advanced feature to categorize notes taken directly in Zotero based on their length:

- **Short Notes Logic:** The logic uses `longShortCutoff = 20` to separate short notes (under 20 words) and embeds them directly into the YAML frontmatter under the `comments:` field.
    
    - **Purpose:** Keeps brief, quick thoughts or immediate reactions about the paper organized in the note's high-level properties.
        
- **Long Notes Logic:** The logic for `longnotes` pulls out longer, reflective notes from Zotero and renders them in a separate callout (`> [!note]- Zotero notes...`) in the body of the Obsidian note.
    
    - **Purpose:** Keeps substantial paragraphs of reflections or summary notes separate from the automated highlights, ensuring they stand out.
        

### 2. Regex Filters for Abstract

The `Abstract` callout uses regular expressions and replacements to structure the text:

Django

```
{{abstractNote|replace("\n","\n>")|striptags(true)|replace("Objectives", "**Objectives**")|replace("Background", "**Background**")...}}
```

- **`|replace("Objectives", "**Objectives**")`:** This is a crucial formatting feature. It looks for standard headings often found in scientific abstracts (like "Objectives," "Background," "Methodology," "Results," and "Conclusion") and wraps them in double asterisks (`**...**`), effectively **bolding** them in the Obsidian output.
    
- **Purpose:** It visually structures the often dense, single-paragraph abstract into readable sections, making it easier to scan the summary and find the key components quickly.
    

### 3. Templater Cursor Sequencing

You have multiple Templater cursor commands (`<% tp.file.cursor(1) %>`, `<% tp.file.cursor(4) %>`) used in the **Key takeaways** and **Processing** fields.

- **Purpose:** When you press the hotkey to jump to the next Templater cursor, it follows the sequence of numbers (1, 2, 3, 4...). This forces you to fill in your high-priority fields first:
    
    1. Jump to **Key takeaways** (`1`) to write your summary.
        
    2. Jump to **Connections** (`4`) to link the paper.
        
- **Workflow:** It ensures you focus on synthesizing information before performing administrative tasks.
    

### 4. Custom Tag Formatter Macro

The code defines a macro called `tagFormatter(annotation)`:

Django

```
{%- macro tagFormatter(annotation) -%}
    {% if annotation.tags -%}
    ...
    {%- endif %}
{%- endmacro -%}
```

- **Purpose:** This macro bundles the complex logic required to check if an annotation has tags and then format those tags correctly for Markdown (`#tag-name`). Instead of writing that logic repeatedly inside the main annotation loop, the template simply calls `{{tagString = tagFormatter(annotation)}}`. This makes the annotation rendering logic much cleaner and easier to maintain.

You should use the double colon (`::`) for **all fields** that you want Dataview to be able to read and query, and only use the single colon (`:`) for static text headers or descriptions that you don't intend to search or filter on.

The fundamental rule for your research setup is: **If you want to query it, use `::`.**

---
## 🔑 Fields Requiring Double Colon (`::`)

The double colon (`::`) creates an **inline field** that is recognizable by the Dataview plugin. You should use it for all the structured, custom metadata that enables your workflow.

|**Field**|**Location in Template**|**Why Use ::**|
|---|---|---|
|**Status**|`Processing` section|Crucial for tracking your workflow (e.g., querying for all papers where `Status:: new`).|
|**Connections**|`Processing` section|Allows Dataview to easily link to related notes or concepts.|
|**Projects**|`Processing` section|Essential for filtering papers by the project they belong to.|
|**Authors**|`Info` callout|Even though authors are in the YAML, formatting them here with `::` allows for inline querying within the body of the note.|
|**Tags**|`Info` callout|While the YAML handles official tags, using `::` here keeps the display consistent with other inline fields.|
|**Collections**|`Info` callout|Allows querying papers based on their Zotero collection.|
|**Page-count**|`Info` callout|Allows querying or sorting by paper length.|
|**Reading-time**|`Info` callout|Allows querying or sorting by estimated time to read.|

