# Automatic Report Generation System

## Purpose
Follow this guide to create a new slide report that matches the structure of past presentations while incorporating the latest data.

## Workflow Overview
1. Convert every source file in `input/data` and `input/template` to Markdown by using markitdown.
2. Draft the new report in Markdown by combining the converted template and data.
3. Export the finished report as a Marp-compatible Markdown file.

## Detailed Instructions

### 1. File Conversion
- Run markitdown for each source file. Example:
  ```
  uvx --from "markitdown[all]" markitdown .\input\data\sample.xlsx -o .\input\data\sample.md
  ```
- Place the Markdown outputs alongside the originals (e.g., `input/data/*.md`, `input/template/*.md`).

### 2. Report Authoring
- Use the converted template Markdown to replicate the slide order, titles, and total slide count.
- Pull figures, tables, and commentary from the converted data Markdown.
- Keep table formats intact when recreating them in the report.
- Insert slide breaks with `---` for every slide.
- When data is missing, write a short, reasonable sentence that keeps the narrative consistent.
- Review the draft to ensure tone and terminology align with previous reports.

### 3. Output Requirements
- Save the final report as `output/output.md` (UTF-8, LF line endings preferred).
- Include Marp front matter if pagination or themes are required (e.g., `marp: true`).

## Additional Notes
- If an instruction is ambiguous, propose one or two alternatives and ask the user which to apply.
- Do not delete or overwrite source files unless explicitly told to do so.
- Document any assumptions made while generating the report.