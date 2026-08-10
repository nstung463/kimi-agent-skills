# Outline Mode Workflow

When the user provides an outline (e.g., per-page content details, structured outline, etc.) and requests generating a PPT based on the outline content, use this mode.

## workflow

Based on the user requirements and audience analysis completed in generate_slides.md step2, proceed with content design.

### step1. Outline Parsing and Understanding

Identify the type of outline the user has provided:
- **Complete outline**: Page-by-page planning with titles, content points, and page types for each page
- **Semi-structured outline**: Provides chapter divisions and key points, but does not explicitly specify page types or per-page allocation
- **Hierarchical tree outline**: Only provides hierarchical topics and subtopics

Understand the following information from the outline:
- Total page count or content volume
- Content allocation per page/section
- Implicit requirements (e.g., whether cover, table of contents, chapter transition pages are needed)

### step2. Content Supplementation Strategy

Decide on the content organization and supplementation approach based on user intent. **Default to Information Supplementation Mode** — only downgrade to a more conservative mode when the user uses explicit restriction keywords. When in doubt, always choose the more actively supplementing mode.

#### [Default] Information Supplementation Mode

Enter this mode whenever no explicit restriction keywords appear:
1. Refer to guideline/search/text_search.md for text supplementation strategies to supplement the outline with content, adding text content, data support, real-world case studies, pros/cons comparisons, arguments and evidence, logical explanations, background information, etc. to enrich the presentation
2. During enrichment, maintain the original outline structure: only enrich the content of each page without changing the original outline plan
3. During the subsequent outline writing process, note what supplementary information was added

> **Note**: Phrases like "help me make a PPT", "make a PPT based on my outline", "work from my outline" **do NOT trigger** Content Adherence or Strict Verbatim mode — they simply mean "use the outline as a foundation" and do not restrict content supplementation. Stay in Information Supplementation Mode.

#### Content Adherence Mode

Only enter this mode when the user explicitly requests that their own content take priority and does not want it significantly changed, e.g.: "use my content as-is", "don't add your own ideas", "don't change what I wrote", "the content cannot change".

Core difference from Information Supplementation Mode: the user's original text is always the primary body of each page; search-supplemented content serves only as supporting material and must not overshadow the original. In this case:
1. Keep the user's core wording, viewpoints, and structure unchanged; refer to guideline/search/text_search.md to search for supporting content (data, case studies, background information, etc.), but search content must serve the user's existing viewpoints — do not introduce new topics or replace the user's narrative direction
2. **Must** actively restructure each page's content visually to prevent blank pages:
  * If the original outline content is too sparse, fill it in through sentence elaboration, logical analysis, and reasonable inference
  * Transform simple text into visual forms (flowcharts, parallel relationships, comparison tables, etc.)
  * May add transitional sentences and explanatory text to make the page content cohesive and complete

#### Strict Verbatim Mode (rare exception)

Only enter this mode when the user uses extremely strong restrictive language, e.g.: "not a single word can be changed", "copy verbatim", "no changes whatsoever allowed". In this case:
1. Present the content of each page exactly as the user provided, with sentence structure strictly following the user's input. However, organize the layout and presentation based on the logical relationships in the content — **it is strictly forbidden to dump all text onto each page without logic!**
2. Supplementing text content through search is strictly forbidden; deleting or expanding sentences is strictly forbidden
3. Estimate the approximate word count for each page in the outline

### step3. Outline Writing

Based on the user's outline and completion results, use the `write_file` tool to construct the presentation outline `outline.md`.

1. **Faithful to user outline**: The outline structure should align as closely as possible with the user's provided outline content, or reflect the user's content planning, without deviating from the user's intent
2. **Information density**: Plan each page's content reasonably, ensuring natural transitions and substantive, in-depth content on each page.
3. **Page types**: Set a type for each page (cover/table_of_contents/chapter/content/final)
4. **Page count requirements**:
  - When the user's outline already has page count requirements, or content is strictly planned per page: Design according to the user's outline page count
  - When the user's outline does not explicitly require page count, but the outline is highly structured: Page count should match the structured design of the outline
  - No page count requirements or structure: Design based on content volume, recommended 12-18 pages; encouraged to include cover, table of contents, chapters, content, and ending pages
5. Chapter consistency: Either set chapter pages for all chapters or for none -- it is strictly forbidden to have transition pages for some chapters but not others

#### Outline Format

```markdown
# Presentation Outline

## Page 1 [cover]
- **Title**: Title of the presentation
- **Content**: Subtitle of the presentation, may be empty

## Page 2 [table_of_contents]
- **Title**: Table of contents heading. e.g., Table of Contents, Executive Overview, etc.
- **Content**: Chapter plan of the presentation. e.g., 1. Chapter One Title; 2. Chapter Two Title, ...

## Page 3 [chapter]
- **Title**: Chapter number and name. e.g., Chapter 1: xxx, 01: xxx
- **Content**: Chapter subtitle or other content to be presented on the page. Ensure the chapter title accurately summarizes all content within that chapter without being overly narrow

## Page 4 [content]
- **Title**: Title of the page
- **Content**: Directly retain the user's original wording, or quote the original points from the corresponding section of the user's outline. If search supplementation was performed, mark supplemented content with "[supplemented]" in the outline
- **Source**: Search information source for supplemented content on this page (annotated with URL), e.g., https://example.com/report-2025

......

## Page x [final]
- **Title**: Title of the ending page
- **Content**: Core viewpoints/insights/inspirations, or thought-provoking questions, or thank-you messages, etc. Determine based on the user's scenario
```

## Writing Guidance for PPTD Generation

1. **Make good use of hyperlinks: When the PPT involves reference materials, further reading, or other external resources, use `<a href="url">` to add hyperlinks to related text, making it convenient for the audience to explore further**
2. Faithful to user outline: Build upon the user's original points cited in the outline without deviating from the outline direction; in Information Supplementation Mode, active expansion is encouraged as long as supplemented content serves the original points without overshadowing them
3. Preserve user wording: Key terms, titles, and expressions from the user's outline should retain the original wording as much as possible, without arbitrary rewording
4. Active expansion: By default, proactively expand key points into in-depth presentation content, supplementing background, data, and case studies; only take a conservative approach when the user explicitly restricts it
5. If the user requires content adherence, each page must still maintain sufficient information density — fill pages through visual restructuring and logical organization; if strict verbatim is required, copy the original text faithfully but with reasonable layout
