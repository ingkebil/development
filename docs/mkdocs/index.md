# How do I publish this manual?

Good. It seems you want to publish your changes?

It is as simple as: 

```
mkdocs gh-deploy
```

Tada! Changes should be available shortly on [http://www.clinicalgenomics.se/development/](https://www.mkdocs.org/user-guide/deploying-your-docs/)

## I want more detail

We are using github's gh-pages to store the generated manual. Once mkdocs has generated HTML from the markdown, it will be stored in the branch `gh-pages`.

More explanation on the [deploying your docs](https://www.mkdocs.org/user-guide/deploying-your-docs/) page.
