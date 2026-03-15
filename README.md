# Journal of Data Science (JDS) Quarto Template

This is a Quarto template for creating manuscripts for submission to the
[Journal of Data Science](https://jds-online.org).
It uses the `jdsart.cls` LaTeX document class (v0.25, maintained by VTeX).

## Creating a New Article

Use this as a template to create an article for JDS:

```bash
quarto use template wenjie2wang/jds.qmd
```

This will install the extension and create an example `.qmd` file and
bibliography that you can use as a starting place for your article.

## Installation for Existing Document

You may also use this format with an existing Quarto project or document.
From the project or document directory, run:

```bash
quarto add wenjie2wang/jds.qmd
```

## Usage

To use the format, specify `jds-pdf` or `jds-html` as the format in your
document YAML:

```yaml
format:
  jds-pdf:
    keep-tex: true
  jds-html: default
```

Or render from the command line:

```bash
quarto render article.qmd --to jds-pdf
```

## Format Options

### Document Class Options

Set via `classoption` in the document YAML:

- `inpress` (default): Single-spaced, 11pt font for final production
- `review`: Double-spaced, 12pt font with line numbers for peer review
- `linenumber`: Add line numbers (automatically enabled in `review` mode)
- `letterpaper` (default) or `a4paper`: Paper size
- `discussion`: For discussion articles
- `chinese`: For Chinese-language articles

For example, to switch to review mode for submission:

```yaml
classoption:
  - letterpaper
  - review
```

### JDS Article Metadata

For accepted articles, set publication metadata:

```yaml
firstpage: 1
month: January
year: 2025
volume: 23
issue: 1
doi: 10.6339/25-JDS1234
```

### Author and Affiliation Format

Authors, affiliations, and footnotes use structured YAML fields that map
directly to `jdsart.cls` commands:

```yaml
title: "My Paper Title"
short-title: "Running Title"  # required, used in page headers
author:
  - first: Adam
    first-init: A.
    last: Ahen
    marker: '1,2'        # affiliation markers
    footnote-id: 1        # optional footnote reference
    email: foo@bar.com    # optional email
footnote:
  - content: Corresponding author
    type: corresp         # set for corresponding author
    id: 1
affiliation:
  - institution: University of Achievement
    prefix: Department A  # optional department/unit
    country: Country A
    marker: 1
```

### Custom LaTeX Preamble

Add additional LaTeX packages via the `preamble` field.
Note that `jdsart.cls` already loads `amsmath`, `amssymb`, `amsthm`,
`graphicx`, `xcolor`, `natbib`, and `hyperref`; the template also loads
`booktabs`, `longtable`, and `array`. You do not need to include these.

```yaml
preamble: |
  \usepackage{tikz}
  \usepackage{algorithm2e}
```

## Shortcodes

The extension provides shortcodes for cross-format markup:

- `{{< latex >}}`: Renders "LaTeX" with proper typesetting
- `{{< proglang R >}}`: Programming language name (e.g., **R**)
- `{{< pkg stats >}}`: Software package name (e.g., *stats*)

In PDF output, these map to `\proglang{}`, `\pkg{}` commands from `jdsart.cls`.
You can also use the raw LaTeX commands directly in PDF-only documents.

## Citations

Use Quarto's native citation syntax. With `cite-method: natbib` (the default
for `jds-pdf`), Quarto automatically converts to natbib commands:

| Quarto syntax | natbib output | Example |
|---|---|---|
| `@key` | `\citet{key}` | Koenker and Bassett (1978) |
| `[@key]` | `\citep{key}` | (Koenker and Bassett, 1978) |
| `[-@key]` | `\citeyear{key}` | (1978) |

This syntax also works for HTML output (via citeproc), so your document
renders correctly in both formats.

## Related

- [jds.rmd](https://github.com/wenjie2wang/jds.rmd): R Markdown template
  for JDS (the predecessor of this Quarto template)
