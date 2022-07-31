# Contributing to AI Singapore's AI Practitioner Handbook

This miscellaneous chapter covers the conventions that were adhered to
in writing this book and how they affect the appearance as well as
standardisation efforts. Aside from ensuring that this book remains
readable and accessible, such conventions would make the process of
maintaining and reviewing contributions manageable. The conventions are
covered across 3 different sections:

- Structure
- Formatting
- Language

To expedite the process for checking if contributions adhere to the
conventions, one can refer to the list below:

__Summary Checklist:__

- No subdirectories are to be created within chapter directories.
- Only Markdown files are to be used for generating content.
- If a Jupyter Notebook is used, use Jupytext pairing function to
  export to MyST flavoured Markdown file. Commit and version both files.
- Ensure headers are in sequential order.
- No manual table of contents.
- Citations and bibliographioes are populated in the centralised
  BibTeX file `book/references.bib` and referred to correctly.
- For language, use Singaporean Standard English.

## Structure

One can refer to this section for the appropriate directories which
files and assets are to be placed under.

### Repository Tree

The tree of the repository containing the book is structured as such:

```
ai-practitioner-handbook
    │
    ├── _config.yml     <-  YAML file detailing configurations for
    │                       Jupyter Book.
    ├── _toc.yml        <-  Configuration file that determines the
    │                       structure of the book.
    ├── .gitignore      <-  File for specifying files or directories
    │                       to be ignored by Git.
    ├── CHANGELOG.md    <-  Text file that lists changes made to the
    │                       project in chronological order.
    ├── CONTRIBUTING.md <-  File specifying conventions and formats
    │                       for contributors' reference.
    ├── README.md       <-  The top-level README containing basic
    │                       information of the project.
    ├── requirements.txt
    │                   ^-  File specifying dependencies needed to
    │                       generate the book.
    │
    ├── .github         <-  Folder (currently) housing workflow
    │                       definitions for GitHub Actions.
    └── book            <-  Directory containing book's contents and
        |                   assets.
        |── assets
        |               ^-  Directory containing non-text assets to be
        |                   referenced by the book.
        └── references.bib
                        ^-  Bibtext file containing citations and
                            bibliographies to be referenced by the book.
```

The files and directory that contributors will be mainly working
with are the following:

- `_toc.yml`
- `requirements.txt`
- `book/**`

Other files or directories are usually not to be modified unless
required and requested by the core reviewers of the book.

### Book Directory & Contents

Most contributions will be populating the `book` directory and mainly
within directories pertaining to the different chapters.

Below describes each of the chapters and their respective
subdirectories:

#### 1. Pre-project Phase

__Directory Name:__ `book/1-pre-project-phase`

__Synopsis:__ *To be filled in...*

__Sections:__

- *Section 1*
- *Section 2*

#### 2. Project Management & Technical Leadership

__Directory Name:__ `book/2-proj-mgmt-tech-lead`

__Synopsis:__ *To be filled in...*

__Sections:__

- *Section 1*
- *Section 2*

#### 3. Collaborative Development Platforms

__Directory Name:__ `book/3-collab-dev-platforms`

__Synopsis:__ *To be filled in...*

__Sections:__

- *Section 1*
- *Section 2*

#### 4. Literature Review

__Directory Name:__ `book/4-lit-review`

__Synopsis:__ *To be filled in...*

__Sections:__

- *Section 1*
- *Section 2*

#### 5. Data Management, Exploration & Processing

__Directory Name:__ `book/5-data-mgmt-exp-proc`

__Synopsis:__ *To be filled in...*

__Sections:__

- *Section 1*
- *Section 2*

#### 6. Modelling

__Directory Name:__ `book/6-modelling`

__Synopsis:__ *To be filled in...*

__Sections:__

- *Section 1*
- *Section 2*

#### 7. Solution Delivery

__Directory Name:__ `book/7-solution-delivery`

__Synopsis:__ *To be filled in...*

__Sections:__

- *Section 1*
- *Section 2*

#### 8. Documentation & Handover

__Directory Name:__ `book/8-documentation-handover`

__Synopsis:__ *To be filled in...*

__Sections:__

- *Section 1*
- *Section 2*

Any new chapters or sections (within a chapter) to be added are to be
subjected to pull requests and further discussions and reviews.
Sections within chapters are all to be structured in a flat manner
and __subdirectories are not to be used__.

## Formatting

This section details the format that contributors can refer to when
contributing content and files to the book.

### Markdown Flavour

This book treats Markdown files as first class citizens with regards
to contents. Meaning: all of the book's contents are to be strictly
derived from
[MyST flavoured Markdown](https://jupyterbook.org/en/stable/content/myst.html#myst-markdown-overview)
files. A contributor may formulate contents within Jupyter Notebooks
(`.ipynb` files) but they would need to do the following:

- Create the Jupyter Notebook under `notebooks`, under the appropriate
  subdirectory corresponding with the chapter it is meant for.
- Its contents are to be converted out to a Markdown file. This can be done with
  [Jupytext](https://jupytext.readthedocs.io/en/latest/index.html),
  through it's
  [paired notebooks functionality](https://jupytext.readthedocs.io/en/latest/paired-notebooks.html).
- In this case, both the paired `.md` and `.ipynb` files are to be
  committed.

### Headers

When using headers, please do use them sequentially.

An example of inappropriate usage:

```markdown
# Top Heading
### Section
```

Appropriate format:

```markdown
# Top Heading
## Section
```

### Table of Contents for Sections

Since Jupyter Book automatically generates table of contents (TOCs) that
appears on either side of the sidebars, manually written TOCs are
unnecessary.

### Citations & Bibliographies

For any part of a content that references to external resources, one is
to ensure that the resource is listed and stored in the BibTeX file
`book/references.bib` in a manner similar to the following:

```bibtex
@article{baker2016reproducibility,
    author = {Baker, Monya},
    title  = {Reproducibility Crisis},
    year   = {2016}
}
```

The resource can be referred to using the following syntax:

```markdown
Results are not as expected {cite:ps}`CITEKEY`.
```

The `CITEKEY` value with reference to the example above would be
`baker2016reproducibility`.

Citation keys are to follow the following convention:

```markdown
`authorYYYYresource_title`
```

__Reference(s):__

- [Jupyter Book Docs - Citations and bibliographies](https://jupyterbook.org/en/stable/content/citations.html#citations-and-bibliographies)
- [`sphinxcontrib-bibtex` Docs](https://sphinxcontrib-bibtex.readthedocs.io/en/latest/)

## Language

For consistency across all chapters, contributors are to stick to the
usage of a single language: Singaporean Standard English, which is
not much different from Standard British English.

Reviewers and contributors are to ensure correct grammar and consistent
tone for contributions. This is a collective effort and everyone has a
part to play in maintaining the quality of the book.

__Reference(s):__

- [Differences between British and American English](https://www.britishcouncilfoundation.id/en/english/articles/british-and-american-english)
