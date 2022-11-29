# How to generate thumbnails of all pages of a PDF with imagemagick

Given a PDF `example.pdf`, I knew that it is possible to export the first page as a PNG with the Imagemagick `convert` command as follows:

```bash
convert example.pdf[0] first_page.png
```

(The above command works in Bash, in Zsh an error is reported: `zsh: no matches found: example.pdf[0]`. If you use Zsh, enclose `example.pdf[0]` in single or double quotes).

For the second page, you would use `example.pdf[1]` and so on.

But I need all the pages! Should I write a loop in the shell and call the `convert` command once for each page? This seems not optimal, because the PDF has to be parsed each time. Surely there is a better way? As expected, Imagemagick has us covered:

```bash
convert example.pdf thumbnail-%03d.png
```

This creates thumbnails named `thumbnail-001.png`, `thumbnail-002.png`, `thumbnail-003.png` and so on. Depending on the number of pages, one could use a different format like `%04d` for four digits in the output filenames or add a directory name to have all thumbnails there:

```bash
convert example.pdf thumbnails/thumbnail-%04d.png
```

I found this trick [here](https://stackoverflow.com/a/5230727)

