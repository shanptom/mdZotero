

# 📄 Writing Articles in RStudio with Zotero Integration

What started as a simple way to take notes quickly evolved into a complete writing workflow.

I first turned to Markdown because it let me combine text and code in one place—no need to jump between apps. As my projects grew more complex, I switched to Quarto Markdown, which allowed me to keep clean, readable documentation with embedded code and commentary—without cluttering the page with endless #Comments.

But the real power of Markdown lies in its flexibility: it supports fully reproducible research. I can publish my scripts and results as HTML, PDF, or Word files. Even better, exporting to MHTML gives me a single, shareable file with interactive plots—perfect for collaboration. With version control baked into RStudio’s Git GUI, I can track changes and back up my work effortlessly.

Managing references used to be the most frustrating part of academic writing—until I discovered Zotero. It’s open-source, powerful, and integrates smoothly with RStudio using the Better BibTeX plugin. No more copy-pasting citations or dealing with proprietary reference managers.

In this post, I’ll walk you through how to combine Markdown, RStudio, and Zotero to build a writing workflow that’s simple, powerful, and reproducible—from your first sentence to your final bibliography.



---

## 🧠 Why This Workflow?

* **Markdown** allows embedding code and text seamlessly.
* **Reproducible research**: Export to HTML, PDF, or Word.
* **Interactive visualizations** via self-contained `.mhtml` files.
* **Built-in Git GUI** in RStudio ensures version control.
* **Zotero** manages references without paywalls or vendor lock-in.

---

## 🔧 Step 1: Install Required Tools

* [📥 Install RStudio](https://posit.co/download/rstudio-desktop/)
* [📥 Install Zotero](https://www.zotero.org/)

---

## 🔌 Step 2: Enhance Zotero with Better BibTeX

### ➕ Install Better BibTeX Plugin

1. **Download Plugin**:
   [Better BibTeX v7.0.26 Release](https://github.com/retorquere/zotero-better-bibtex/releases/tag/v7.0.26)

2. **Install in Zotero**:

   * Go to `Tools → Plugins → ⚙️ Gear Icon → Install Add-on From File`
   * Select the downloaded `.xpi` file
   * Restart Zotero

---

### ⚙️ Configure Better BibTeX

1. **Open Settings**:
   `Edit → Preferences → Better BibTeX`

2. **Set Citation Key Formula**:

   ```plaintext
   [auth.etal:lower:replace=.,_:postfix=_][>0][year]|[veryshorttitle][year]
   ```

---

## 🔄 Step 3: Connect Zotero with RStudio

### 📦 Install `rbbt` R Package

```r
# Install rbbt from GitHub
if (!require("remotes")) install.packages("remotes")
remotes::install_github("paleolimbot/rbbt")
```

---

### ⌨️ Add Keyboard Shortcut

1. Go to `Tools → Modify Keyboard Shortcuts...`
2. Search: `"Zotero"`
3. Locate: **Insert Zotero Citation**
4. Assign shortcut (e.g., `Ctrl + L` or `Cmd + L`)
5. Click **Apply**

---

## 📝 Step 4: Create Your Quarto Markdown Template

### Example YAML Header:

```yaml
title: "Article Title"
author: "Author Name"
date: "`r Sys.Date()`"

output:
  html_document:
    code_folding: hide    
    code_download: false

knitr:
  echo: false
  warning: false
  message: false
  fig.width: 15
  fig.height: 6

editor: visual

bibliography: "`r rbbt::bbt_write_bib('bibliography.json', overwrite = TRUE)`"
```

---

## 🔁 Step 5: Cite As You Write

* Press your shortcut (e.g., `Ctrl+L`)
* Search and insert Zotero references
* Let RStudio handle:

  * In-text citations
  * Bibliography generation
  * `.json` citation file

---

## 🧩 Behind the Scenes

1. First citation:

   * Creates `bibliography.json`
   * Adds formatted bibliography section

2. Later citations:

   * Automatically appended
   * Deduplicated

3. Final output:

   * References in APA, Chicago, etc.
   * Fully reproducible and clean document

---

## 🙏 Acknowledgments


Inspired by community contributions from:

* @Verhoeven
* @Rioja
* @Dunnington

---

## 📚 References
1. Dunnington, Dewey. 2020. “Getting Started with Zotero, Better BibTeX, and RMarkdown.” May 9, 2020. https://dewey.dunnington.ca/post/2020/getting-started-zotero-better-bibtex-rmarkdown/.

2. Rioja, Kenneth. (2023) 2025. “Kennethrioja/Rmdzoteroword_workflow.” Shell. https://github.com/kennethrioja/rmdzoteroword_workflow.

3. Verhoeven, Gertjan. 2021. “Writing Scientific Papers Using Rstudio and Zotero.” Gertjan Verhoeven. May 2, 2021. https://gsverhoeven.github.io/post/zotero-rmarkdown-csl/.
