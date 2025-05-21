

# 📄 Writing Articles in RStudio with Zotero Integration

I started using Markdown as a note-taking tool mainly because it let me combine text and code in one place, without needing to switch between different applications. Eventually, I moved on to Quarto Markdown for a cleaner UI. It allowed me to write explanatory notes right next to the code, keeping everything clean and readable without the need for cluttered #comments.

One of the things I like most about Markdown is its flexibility—it supports reproducible research. I can share both the code and results in different formats like HTML, PDF, or Word. For easier sharing, I often save HTML files as MHTML, so I have a single self-contained file with scripts and results in interactive visualizations. This makes collaboration much smoother. On top of that, RStudio’s built-in Git GUI makes version control and backups easy, which helps maintain the integrity of my projects.

For reference management, I rely on Zotero. It’s a solid open-source tool that avoids the restrictions of proprietary alternatives and handles citations well. With plugins like Better BibTeX, it integrates nicely with RStudio, making bibliography management in academic writing much more efficient.

In this post, I’ll go through how to write articles/manuscripts in RStudio using Markdown and manage references with Zotero, all within a workflow that’s clean, efficient, and reproducible.


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
