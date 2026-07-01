# 🖨️ How to Make a PDF from These Notes

Turn the whole notes repository into a **single PDF** for offline reading.

---

## Option 1 — VS Code Extension (easiest, no install)

1. Install the **"Markdown PDF"** extension by *yzane* in VS Code.
2. Open any `.md` file.
3. Right-click → **"Markdown PDF: Export (pdf)"**.
4. A PDF is created next to the file.

> To combine everything into one PDF, first merge the files (see Option 3), then export.

---

## Option 2 — Pandoc (best quality, one command)

**Install Pandoc** (https://pandoc.org/installing.html) and a LaTeX engine (e.g., MiKTeX on
Windows). Then from the `Backend-Interview-Notes` folder run:

```powershell
# Combine ALL markdown files into one PDF (PowerShell)
$files = Get-ChildItem -Recurse -Filter *.md | Sort-Object FullName
pandoc $files.FullName -o Backend-Interview-Notes.pdf `
  --toc --toc-depth=2 -V geometry:margin=1in -V fontsize=11pt
```

- `--toc` adds a table of contents.
- Works great with the Mermaid/ASCII diagrams (ASCII renders as-is).

---

## Option 3 — Merge into one Markdown, then export

```powershell
# Merge all .md files into one big file
Get-ChildItem -Recurse -Filter *.md |
  Sort-Object FullName |
  ForEach-Object { "`n`n---`n`n"; Get-Content $_.FullName } |
  Set-Content ALL-NOTES.md
```
Then export `ALL-NOTES.md` with Option 1 or 2.

---

## Option 4 — md-to-pdf (Node.js)

```powershell
npm install -g md-to-pdf
md-to-pdf ALL-NOTES.md      # creates ALL-NOTES.pdf
```

---

## 💡 Tips
- For **Mermaid diagrams** to render as images, use the *Markdown Preview Mermaid Support*
  extension or Pandoc with `mermaid-filter`.
- Keep the folder order (numbered files) so the PDF flows logically.
- Export the `CheatSheets/` folder alone for a **short revision PDF**.

[⬅ Back to Cheat Sheets Index](./README.md)

