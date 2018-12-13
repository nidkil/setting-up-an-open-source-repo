# markdown-toc

A very simple but effective tool that generates a table of contents (toc) from the headings in a markdown file and adds it to the file.

1. Install the `markdown-toc` package.

    ```bash
    $ npm install --save-dev markdown-toc
    ```

2. Add the following entry to `scripts` in the `package.json` file.

   ```json
   {
     "scripts": {
       "readme:toc": "markdown-toc README.md -i --no-firsth1 --maxdepth=1 --bullets=-"
     }
   }
   ```

2. Add the markdown-toc `<!-- toc -->` marker to the `README.md` file that indicates where the toc must be inserted.

    In the following example header 2 & 3 are added to the toc when `readme:toc` is run. The html tags `<details>` around the toc makes the toc collapsible. If you do not want this leave them out.

    ```md
    # Page header

    <details>
      <summary><strong>Table of Contents</strong> (click to expand)</summary>
      <!-- toc -->
    </details>

    ## Header 1 toc

    ### Subheader not part of toc

    ## Header 2 toc
    ```

