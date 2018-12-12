# JSDoc

Code that you wrote 6 months ago is often indistinguishable from code that someone else has written. You will look at it with a fond sense of remembrance. Then a sneaking feeling of foreboding, knowing that someone less experienced, less wise, had written it.

As you go through the selfless act of untangling things that were obvious or clever months ago, you will start to empathize with your users. If only you had written down **_why_** you had done something. Life would be so much simpler :-( Documentation allows you to transfer the **_why_** behind the code. Much in the same way code comments explain the **_why_**, and not the **_how_**, documentation serves the same purpose.

The de facto standard for documenting JavaScript code is [JSDoc](http://usejsdoc.org/). We will install and configure the module.

1. Install the `jsdoc` module.

    ```bash
    $ npm install --save-dev jsdoc
    ```

2. Add a basic `jsdoc.config.js` configuration file to the root directory of the project with the following contents.

   ```json
   {
     "plugins": [],
     "recurseDepth": 10,
     "source": {
       "include": ["src"],
       "exclude": [],
       "includePattern": ".+\\.js(doc|x)?$",
       "excludePattern": "(^|\\/|\\\\)_"
     },
     "sourceType": "module",
     "tags": {
       "allowUnknownTags": true,
       "dictionaries": ["jsdoc", "closure"]
     },
     "templates": {
       "cleverLinks": false,
       "monospaceLinks": false
     }
   }
   ```

   > The important part here is the entry point where JSDOc starts generating the documentation, which is specified in `source`. Please refere to the JSDocs [here](http://usejsdoc.org/about-configuring-jsdoc.html) for further information about the available configuration options.

3. Add the following section to your package.json:

   ```json
   {
     "scripts": {
       "gendocs": "jsdoc -r -c jsdoc.config.json -d ./docs"
     }
   }
   ```

   > The important part here is the `-r` recurse flag, which makes sure JSDoc recursively iterates the directories to the depth specified in `recurseDepth` (see `jsdoc.config.json`) when generating the documentation. Please refer to the JSDocs [here](http://usejsdoc.org/about-commandline.html) for further information about the available commandline arguments.

   Now all you have to do is run `npm run gendocs` or `yarn gendocs` to generate your project's documentation.

Now start adding JSDoc comments to your code :-)
