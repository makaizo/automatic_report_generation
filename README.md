# Automatic Report Generation Toolkit

This repository shows how to reproduce slide reports from previous projects by combining historical templates with new data. The workflow relies on [markitdown](https://github.com/microsoft/markitdown) to convert Excel and PowerPoint files into Markdown and on [Marp](https://marp.app/) to turn the final Markdown back into presentation slides.

![Workflow diagram](./images/flow.drawio.svg)

## Repository Layout
- `input/template/` – Original PowerPoint templates.
- `input/data/` – New data sources (e.g., Excel files).
- `output/` – Destination for the generated Marp Markdown reports.
- `Agents.md` – Step-by-step instructions for AI coding agents.
- `n8n_workflow.json` – Optional automation workflow for n8n users.

## Prerequisites
- [uv](https://github.com/astral-sh/uv) to run markitdown via `uvx`.
- [Marp VS Code extension](https://github.com/marp-team/marp-vscode) or [Marp CLI](https://github.com/marp-team/marp-cli).

## Two Options for Report Generation
1. **VSCode + AI Agent** (claudecode, codex, cline, etc.):
   you have to write the prompt and convert files manually but this it more flexible.
2. **n8n Workflow**:
   you can run the entire workflow automatically but this is less flexible.

## Option 1: VS Code + AI Agent

1. **Open this repo in VS Code.**
2. **Place your new data files** (e.g., `survey.xlsx`) in `input/data/` and your template files (e.g., `template.pptx`) in `input/template/`.
3. **Launch your coding agent extension** (Claude Code, Codex, Cline, etc.) and share the prompt:
   ```
   can you make a new report using @input/template/xxx and @input/data/xxx?
   please follow the instructions in @Agents.md carefully.
   ```
4. **Convert files and check the output**
preview the generated `output/output.md` in Marp VS Code extension. you can adjust wording or formatting manually if needed.

## Option 2: n8n Workflow

1. **Install and start n8n.**
   ```
   npx n8n
   ```
2. **Import** `n8n_workflow.json` into your n8n instance.
3. **Run markitdown-mcp as a service** so the workflow can access conversion tools:
   ```
   markitdown-mcp --http --host 127.0.0.1 --port 3001
   ```
   Test the service with `curl` if needed.
4. **Execute the workflow** inside n8n to produce the Markdown report in `output/`.
5. **Export the final slides with Marp** as described above (n8n’s Execute Command node cannot run Marp-cli reliably, so this step remains manual).

## Tips
- If requirements change, update `Agents.md` so future reports follow the new rules.