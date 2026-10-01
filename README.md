# markdown-cv

A curriculum vitae maintained in plain text and rendered to HTML and PDF using CSS.

For more details, see the [project page](http://elipapa.github.io/markdown-cv), or the blog post on [why I switched to markdown for my CV](http://elipapa.github.io/blog/why-i-switched-to-markdown-for-my-cv.html).

***

## Customization

Simply [fork the markdown-cv repo](https://github.com/elipapa/markdown-cv)

![](https://help.github.com/assets/images/help/repository/fork_button.jpg)

and edit the `index.md` file [directly in Github](https://help.github.com/articles/editing-files-in-your-repository/)

![](https://help.github.com/assets/images/help/repository/edit-file-edit-button.png)

adding your skills, jobs and education.

![](https://help.github.com/assets/images/help/repository/edit-readme-light.png)

## Distribution

To transform your plain text CV into a beautiful and shareable HTML page, you have two options:

### I. Use Github Pages to publish it online

1. Delete the existing `gh-pages` branch from your fork. It will only contain this webpage. You can either use git or [the Github web interface](https://help.github.com/articles/creating-and-deleting-branches-within-your-repository/#deleting-a-branch).
2. Create a new branch called `gh-pages`.
3. Head to *yourusername*.github.io/markdown-cv to see your CV live.

Any change you want to make to your CV from then on would have to be done on the `gh-pages` branch and will be immediately rendered by Github Pages.

### II. Build it locally and print a PDF

1. To [install jekyll](https://jekyllrb.com/docs/installation/), run `gem install bundler jekyll` from the command line.
3. [Clone](https://help.github.com/en/articles/cloning-a-repository) your fork of markdown-cv to your local machine.
3. Type `jekyll serve` to render your CV at http://localhost:4000.
4. You can edit the `index.md` file and see the changes live in your browser.
5. To print a PDF, press <kbd>⌘</kbd> + <kbd>p</kbd>. Print and web CSS media queries should take care of the styling.

## Export to Word

The Python exporter reads `index.md` and creates an editable `.docx` with the
project photo, headings, bullet lists, and working hyperlinks. The Markdown is
the source of truth: regenerating a Word file replaces edits made only in Word.
The Word layout is a simple single-column CV, independent of the website CSS.

Requires Python 3.10 or newer. On Windows, from the repository directory:

```powershell
py -3 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements-docx.txt
.\.venv\Scripts\python.exe scripts/export_docx.py
```

On macOS/Linux, use `python3 -m venv .venv` and `.venv/bin/python` instead.
Microsoft Word, LibreOffice, and Jekyll are not required for export.

Language is detected from the CV. Defaults are `build/cv-en.docx` on `gh-pages`
and `build/cv-it.docx` on `gh-pages-ita`. Generated files are ignored by Git.

```powershell
# A4 paper, custom output, or a version without a photo
.\.venv\Scripts\python.exe scripts/export_docx.py --page-size a4 --output build/curriculum.docx
.\.venv\Scripts\python.exe scripts/export_docx.py --no-photo

# Export the Italian worktree from the English repository
.\.venv\Scripts\python.exe scripts/export_docx.py --input ../curriculum-ita/index.md
```

Use `--photo path/to/image.jpg` to replace the portrait or `--language en|it`
to override detection. Paper defaults to Letter; pass `--page-size a4` for A4.
Inspect the generated file in Word before sending it, especially after adding
content. The exporter supports this CV's headings, paragraphs, bold/italic text,
links, date spans, bullet lists, contact HTML, and `<br>` breaks. It reports an
error for unsupported Markdown instead of silently dropping content.

Keep `scripts/export_docx.py`, `requirements-docx.txt`, the export instructions,
and shared styles identical on both language branches. Translate only CV content.

Run the content-preservation checks with:

```powershell
.\.venv\Scripts\python.exe -m unittest discover -s tests -v
```

## Styling

The included CSS will render your CV in two styles:
s
1. `kjhealy` the original default, inspired by [kjhealy's vita
template](https://github.com/kjhealy/kjh-vita).
2. `davewhipp` is a tweaked version of `kjhealy`, with bigger fonts and dates
  right aligned.

To change the default style, simply change the variable in the
`_config.yml` file.

Any other styling is possible. More CSS style contributions and forks are welcome!

### Author

Eliseo Papa ([Twitter](http://twitter.com/elipapa)/[Github](http://github.com/elipapa)/[Website](https://elipapa.github.io)).

![Eliseo Papa](https://s.gravatar.com/avatar/eae1f0c01afda2bed9ce9cb88f6873f6?s=100)

### License

[MIT License](https://github.com/elipapa/markdown-cv/blob/master/LICENSE)
