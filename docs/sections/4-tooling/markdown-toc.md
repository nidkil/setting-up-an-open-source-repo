# markdown-toc

A very simple and effective tool that generates a table of contents (toc) from the headings in a markdown file and adds it to the file.

## Setup

1. Install the `markdown-toc` package.

    ```bash
    $ npm install --save-dev markdown-toc
    ```

2. Add the following entry to `scripts` in the `package.json` file.

   ```json
   {
     "scripts": {
       "readme:toc": "markdown-toc README.md -i --maxdepth=2 --bullets=-"
     }
   }
   ```

    If you want to exclude the first header just add the option `--no-firsth1`. The option `maxdepth` determines to which header level to include.

2. Add the markdown-toc `<!-- toc -->` marker to the `README.md` file that indicates where the toc must be inserted.

    In the following example header 2 & 3 are added to the toc when `readme:toc` is run. The html tags `<details>` around the toc makes the toc collapsible and there are links back to the index. If you do not want this then just ommit them (see next example).

    ```md
    # Page header

    <a name="toc">
      <details>
        <summary><strong>Table of Contents</strong> (click to expand)</summary>
          <!-- toc -->
      </details>
    </a>

    ## Header 1 toc

    ### Subheader not part of toc

    [Go to Table of Contents](#toc)

    ## Header 2 toc

    [Go to Table of Contents](#toc)
    ```

    Example of the toc that is not collapsible.

    ```md
    # Page header

    <a name="toc">
      <strong>Table of Contents</strong>
      <!-- toc -->
    </a>

    ## Header 1 toc

    ### Subheader not part of toc

    [Go to Table of Contents](#toc)

    ## Header 2 toc

    [Go to Table of Contents](#toc)
    ```
