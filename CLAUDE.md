# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **client-side Markdown-to-Medium converter** - a standalone HTML application that converts Markdown content into Medium.com-compatible HTML. The entire application is self-contained in a single HTML file with embedded CSS and JavaScript.

**Key characteristic:** This is a pure static HTML application with no build process, dependencies, or server components. Everything runs in the browser.

## Core Architecture

### Single-File Architecture

The main file `markdown-to-medium_EN.html` contains:
- **HTML Structure:** Split-pane layout with Markdown input (left) and live preview (right)
- **Embedded CSS:** Complete styling including responsive design and platform-specific adjustments
- **Embedded JavaScript:** All conversion logic and UI interactions

### The Conversion Pipeline

The core conversion function `markdownToMediumHTML()` uses a multi-stage placeholder system to handle complex edge cases:

1. **Step 1 (Lines 384-421):** Code block protection via placeholders
   - Empty lines → `AAAAAAAAAAAAAAAAAAAAAA` placeholder
   - Hash symbols (`#`) → `HASH_PLACEHOLDER`
   - List symbols (`-`) → `LIST_SYMBOL_PLACEHOLDER`
   - These prevent Markdown processor from misinterpreting code content

2. **Step 2 (Line 424):** Convert code blocks to `<pre><code>` tags

3. **Step 3 (Lines 428-478):** Process Markdown elements
   - Inline code, bold, italic formatting
   - Headers (h2, h3, h4)
   - Blockquotes, links, horizontal rules
   - Ordered and unordered lists
   - Paragraph wrapping

4. **Step 4 (Lines 480-488):** Cleanup and placeholder restoration
   - Remove empty `<p>` tags
   - Remove unwanted breaks after headers
   - Restore placeholders to original content

### Platform-Specific Handling

The application detects macOS vs non-macOS environments (lines 323-327, 509-548):
- **macOS:** Uses `navigator.clipboard.writeText()` with additional HTML cleanup
- **Non-macOS:** Uses legacy `document.execCommand("copy")` method
- **Firefox/Others:** Manual copy instructions displayed

## Development Workflow

### No Build Process Required

This project has **no build, compile, or dependency management steps**. To work with it:

1. **Testing Changes:** Simply open `markdown-to-medium_EN.html` in a browser
2. **Live Development:** Use browser DevTools to test JavaScript/CSS changes
3. **Making Changes:** Edit the HTML file directly - all code is embedded

### Testing the Converter

To verify the conversion logic works correctly:

1. Open the HTML file in multiple browsers (Chrome, Firefox, Safari)
2. Test with complex Markdown containing:
   - Code blocks with empty lines (YAML, Docker Compose)
   - Code blocks with headers (`# Step 1` in bash scripts)
   - Code blocks with list symbols (`- item` in code examples)
   - Mixed content (text, code, lists, headers)
3. Copy the output and paste into Medium.com to verify formatting

### File Organization

- **Production file:** `/workspace/markdown-to-medium_EN.html` (592 lines)
- **Archive/Development:** `/workspace/Arbeitsdaten/` contains older versions and test files
- **Documentation:** `/workspace/README.md` contains comprehensive project documentation

## Critical Implementation Details

### The Placeholder System

The placeholder approach is **essential** to prevent the Markdown processor from misinterpreting code block content:

- Code blocks are extracted and protected BEFORE Markdown processing
- Unique placeholder strings must not appear in normal Markdown content
- Placeholders are restored AFTER all Markdown conversions complete
- Order matters: protection → conversion → restoration

### Known Edge Cases Handled

1. **Empty lines in code blocks:** Preserved using `AAAAAAAAAAAAAAAAAAAAAA` (lines 384-393)
2. **Headers in code:** Hash symbols protected before header regex runs (lines 395-407)
3. **Lists in code:** List symbols protected before list regex runs (lines 409-421)
4. **Spacing after headers:** Removed at both Markdown level (line 381) and HTML level (lines 481-483)
5. **Platform-specific clipboard:** Different copy mechanisms for macOS/Windows/Linux (lines 505-548)

### Regex Processing Order

The order of regex replacements is critical:

1. Code block placeholders MUST be applied first
2. Code block conversion happens before inline formatting
3. Headers processed in reverse size order (### before ## before #)
4. Lists processed after headers to avoid conflicts
5. Paragraph wrapping happens last

## Localization Notes

- **English version:** `markdown-to-medium_EN.html` (current, maintained)
- **German version:** Deprecated per README (line 10)
- UI strings are hardcoded in HTML/JavaScript (lines 330-374)

## Browser Compatibility

- **Chrome/Edge:** Full support including one-click copy
- **Firefox:** Manual copy required (CTRL+C)
- **Safari/macOS:** Uses Clipboard API with additional cleanup
- **Mobile:** Responsive design supports small screens (media queries at lines 197-225)

## Important Constraints

1. **No external dependencies:** All code must remain self-contained in the HTML file
2. **No server processing:** All conversion happens client-side in JavaScript
3. **Backwards compatibility:** Must work in older browsers without modern JS features
4. **Medium.com compatibility:** Output HTML must paste cleanly into Medium's editor

## Common Modification Scenarios

### Adding New Markdown Syntax

1. Add placeholder protection if syntax could appear in code blocks
2. Add regex pattern in the formatting section (after line 428)
3. Ensure regex doesn't conflict with existing patterns
4. Test with code blocks containing the new syntax

### Adjusting Output Styling

1. Modify preview CSS (lines 227-318) for visual appearance in the tool
2. Remember: Final Medium.com rendering may differ from preview
3. Test actual Medium paste behavior, not just preview

### Fixing Copy/Paste Issues

1. Platform detection logic: lines 323-327, 509
2. macOS cleanup: lines 517-533
3. Windows/Linux fallback: lines 535-548
4. Add new cleanup regex patterns at lines 521-528 if needed
