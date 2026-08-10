# Editing User-Uploaded Presentations

Read this guide when a user uploads a pptx file and requests **modifications** to its content, style, or structure.

- If the user uploads a PPT as a template/reference for creating a new presentation (e.g., "use this PPT as a template to make a new one", "create a PPT about xxx referencing this style"), follow the generation workflow in generate_slides.md (template mode), not this guide.
- If the user makes vague modification requests like "beautify this PPT" or "adjust the design of this PPT", always follow the generate_slides.md generation flow, not this guide.

## step1: Understand User Requirements

Clarify what the user wants to modify:
- **Content modification**: Change text, update data, add/remove pages
- **Style modification**: Change color scheme, fonts, layout
- **Structure modification**: Adjust page order, merge/split pages
- **Mixed modification**: Combination of the above

## step2: Understand PPTX Content as Needed

Choose the lowest-cost reading method based on the scope of modifications, avoiding unnecessary context consumption:

### Targeted Modification (Modifying content/style of specific pages)
1. First use `read_file` to quickly understand the content structure, locate the page and position of the text to be modified, then use `scripts/screenshot.sh` to view the visual effect of the corresponding pages, ensuring reasonable visual results during the modification process

### Batch Modification (Batch replacing elements, global style adjustments, etc.)
2. If you need to batch modify certain elements (e.g., batch replace logos, batch adjust font sizes, etc.), first use `scripts/screenshot.sh` to view screenshots and find these elements, then use `scripts/convert.sh` to convert to pptd format, read the corresponding pages to find element commonalities (e.g., all pointing to the same image src, all using the same text style, etc.), facilitating subsequent batch replacement using Grep and other commands.

### Large-Scale Modification (Many pages, global style change/layout beautification, etc.)
3. When the PPT has many pages (e.g., 30+ pages) and requires global modifications, adopt a **sampling survey** strategy to avoid consuming large amounts of context by reading page by page:
   - First use `scripts/screenshot.sh` to sample a few pages (e.g., first page, middle page, last page) to quickly understand the overall style and layout patterns
   - Then use `scripts/convert.sh` to convert to pptd format, and use Grep to batch analyze common patterns (e.g., color schemes, font sizes, layout structures across all pages)
   - Based on sampling results, formulate unified modification rules rather than customizing solutions page by page
   - If layout beautification is needed, sample to determine which page types have suboptimal layouts, formulate optimization standards, and delegate to sub-agents for parallel execution in step5

## step3: Convert to PPTD

```bash
scripts/convert.sh input.pptx -o output_dir/
```

After conversion, the following will be generated under `output_dir/`:
- `*.pptd` main entry file (containing size, theme, and page path list)
- `pages/*.page` page files (one `.page` file per page)
- `images/` directory (extracted image resources)
- `fonts/` directory (extracted embedded fonts)

## step4: Locate Target Content

### Location Strategy

1. Locate by page
Read the main entry file to understand the page order: `output_dir/*.pptd`
List all page files: `Glob: pattern="output_dir/pages/*.page`

2. Locate by element ID: Search within pages: `Grep: pattern="elementId: title_1" path=output_dir/pages/`

3. Locate by text content: Search for the text to modify in the pages directory: `Grep: pattern="market size" path=output_dir/pages/`

4. Locate by element type: `Grep: pattern="elementType: chart" path=output_dir/pages/`

5. Locate by style: Search for color, font size, and other style properties: `Grep: pattern="#FF5733" path=output_dir/pages/`

### Detailed Reading After Location

After finding the target page, directly read the `.page` file to get the complete page structure.

## step5: Modify PPTD

Choose the execution method based on the modification scale:

### Small-Scale Modification (< 10 pages)

The main agent directly uses the `edit_file` tool to make precise modifications to the PPTD files:

- **Modify page content**: Modify page text, elements, element properties, etc. — simply find the corresponding location and edit
- **Modify theme**: The main entry file contains the theme definition. First determine whether the modification can be achieved quickly by modifying the theme definition
- **Delete pages**: Remove the corresponding `.page` file from the `pages` list in the main entry `.pptd`, and delete that file
- **Add pages**: Add the new page's relative path to the `pages` list in the main entry `.pptd`, and create a new `.page` file in the `pages/` directory
- **Adjust page order**: Modify the order of paths in the `pages` list of the main entry `.pptd`

### Large-Scale Modification/Addition (>= 10 pages)

When batch modifying large numbers of pages (e.g., global style change, batch layout beautification) or batch adding pages, use multi-agent parallel processing:

1. Use create_subagent to create sub-agents: Create 1 sub-agent per 20 pages. The following information must be declared when creating:
  * The identity is a **pptx page editing sub-agent** (not the main agent)
  * The goal is to modify/add x .page files
  * The following content must be read before execution for guidance:
    a. {skill_path}/format/pptd.md: Format definition of the pptd file
    b. The converted .pptd main entry file and related .page files
    c. {skill_path}/guideline/subagent/attention.md: Notes for creating presentations

2. The following information must be declared when assigning tasks to sub-agents:
  * Which pages to modify/add: Directly specify the corresponding .page file names
  * Specific modification rules: Such as unified color scheme change, layout style adjustment, font replacement, and other clear modification standards
  * For new pages: Follow the sub-agent task assignment approach in generate_slides.md step5, providing content sources and writing guidance


## step6: Check Modified PPTD

After modifications are complete, run the checker to ensure no new issues were introduced:

```bash
scripts/check.sh output.pptd
```

- Fix all ERRORs first (format errors, invalid references, etc. — failure to fix will cause conversion failure)
- Then handle WARNINGs: **PPTD renders precisely and will not automatically scale text or adjust layouts. Every WARNING reported by the checker means the final PPTX will have a corresponding visual issue (truncation, occlusion, overflow, etc.) that will not be auto-corrected.** Therefore, WARNINGs must be fixed by default, unless you can clearly determine the WARNING is part of the intended design (e.g., decorative elements intentionally extending beyond the canvas). If skipping a WARNING, you must explain the reason for skipping.
  1. TextOverflowWarning (text overflow): Text content requires more space than the text box provides, causing content truncation (must fix unless it existed in the user's original pptx)
  2. TextOcclusionWarning (text occlusion): Text is occluded by other elements, making text unreadable
  3. TextDriftWarning (text drift): Text box is not fully aligned with underlying elements
  4. TextUnderfillWarning (text underfill): Text box is too large or font size too small, causing large blank areas
  5. BoundsOutsideWarning (out of bounds): Element is partially or fully outside the canvas
- **Parallel fixing**: **Must call the edit_file tool in parallel as many times as possible in a single response**, fixing issues across multiple files at once, rather than fixing files one by one sequentially.
- Repeat checking until all ERRORs are eliminated and unexpected WARNINGs are handled

## step7: Deliver

- **In-place delivery — do not copy the .pptd file alone.** .pptd depends on sibling `pages/`, `images/`, etc. in the same directory; `cp`-ing the entry file by itself will cause the Artifact Output to fail to render. If relocation is required, migrate the entire directory (not just the .pptd).
- Inform the user that modifications are complete, and summarize what changes were made
- Inform the user they can click the card in the conversation to view and download the presentation in pptx format

## Few Shot

### Case 1
- User query: Keep every word of the text content, make the PPT look beautiful
- Model actions: Do not follow the edit_user_slides.md flow; read generate_slides.md and follow the generation flow

### Case 2
- User query: This is the old version of my defense PPT; read my latest version of the paper and update the defense PPT content to match the latest version
- Model actions:
  1. Read the latest version of the paper
  2. Use the read_file tool to read the PPT and get the text content (in markdown format)
  3. Compare the PPT content with the paper, analyze what needs to change (e.g., the literature review section doesn't match the paper and needs a complete revision)
  4. Use the screenshot script to capture all pages of the relevant chapters, understand which text boxes and images are involved, and whether pages need to be added or removed
  5. Use the convert script to convert the pptx to pptd
  6. Read the relevant pages and make content modifications
  7. Use the check script to validate and fix issues

### Case 3
- User query: Add a logo to the top-right corner of all content pages
- Model actions:
  1. Use the read_file tool to read the PPT and get the text content (in markdown format)
  2. Analyze the content to determine which pages are content pages
  3. Use the screenshot script to capture the relevant pages and identify a suitable blank area
  4. Use shell commands to batch-add the logo to those pages
  5. Review screenshots of some modified pages to verify the position and size look right
  6. Use the check script to validate and fix issues
