# docsify

`docsify` is a tool to quickly and easily add documentation to any project and publish it to [GitHub Pages](https://pages.github.com/). It makes maintaining documentation a breeze, especially when it starts growing.

1. Install `docsify` globally.

    ```bash
    $ npm install -g docsify-cli
    ```
    
2. Initialize `docsify` in the `docs` directory by executing the following command in the root directory of the project.

    ```bash
    $ docsify init docs
    ```

    After the init is complete, the following files will be in the `docs` directory.

    ```bash
    index.html - the entry file that contains the configuration object `window.$docsify = {}`.
    README.md  - the home page, which is the entry page to the documentation
    .nojekyll  - prevents GitHub Pages from ignoring files that begin with an underscore
    ```

    You can easily update the documentation in in the `README.md` file.
    
3. Structure the documentation by adding a sidebar and additional pages.

   Adding additional pages is as easy as creating additional markdown files in the `docs` directory. When you have a lot of documentation (like this repository) then it is a good idea to structure the markdown files to make it easy to find and edit pages. It also helps keep an overview and simplifies reorganizing the documentation.
   
   To give you a concrete example we will setup the structure and sidebar as it is used by this repository. 
   
   Lets create a `sections` directory with a number of subdirectories that looks like the following structure.
   
   ```bash

   ``` 

4. Add a cover page.



5. Time to preview the `docsify` site.

   Run the local server with `docsify serve docs`. You can preview the site by going to `http://localhost:3000` in the browser.

   ```bash
   $ docsify serve docs
   ```
    
   For convenience add the command to the `scripts` in the `package.json` file.

   ```json
   {
      "scripts": {
        "docs": "docsify serve docs"
      }
   }
   ```

Checkout the `docsify` documentation [here](https://docsify.js.org) for more information how to configure it and other options.

## Preparing GitHub Pages

GitHub Pages is a static site hosting service designed to host personal, organization, or project pages directly from a GitHub repository. It is free and it works with docsify :-)

SO lets get it up and running. Execute the following steps.

1. Enable GitHub Pages

    Adding GitHub pages to an existing repository is very easy.

    - Login to your [GitHub](https://github.com) repository
    - Select the `Settings` tab
    - Scroll down the page that is displayed and look for `GitHub Pages`
    - From the `Source` dropdown select `master branch /docs folder`
    - Click save
    
    Your side is now available at [https://nidkil.github.io/setting-up-an-open-source-repo](https://nidkil.github.io/setting-up-an-open-source-repo/)! How easy is that?

## Custom domain

Optionally you can setup a custom domain to GitHub Pages.

> **Note** there are many ways to set this up. I have chosen to use a subdomain. Please refer to the GitHub Pages documentation [here](https://help.github.com/articles/using-a-custom-domain-with-github-pages/) to read more about the other options.
    
Wouldn't it be cool if you could add your own domain? Well you can. If you have a domain and have access to the DNS then setting a custom domain up is very easy.

1. Create DNS entry
    
    You need to have or purchase a custom domain. Login to the DNS of your domain host and add a CNAME record with the following information.
    
    - Subdomain: setting-up-an-open-source-repo.nidkil.com
    - Point to: nidkil.github.io
    
    DNS changes can take over a full day to update, and the wait varies among DNS and hosting providers.

2. Enable the custom domain to the GitHub repository.

    - Login to your [GitHub](https://github.com) repository
    - Select the `Settings` tab
    - Scroll down the page that is displayed and look for `GitHub Pages`
    - Enter your custom domain in the `Custom domain` text field.
    - Click save
    - In the field custom domain enter your custom domain, e.g. `setting-up-an-open-source-repo.nidkilc.om`
    
