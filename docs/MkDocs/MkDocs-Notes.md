# MkDocs
--------

MkDocs is a static site generator written in python language. It uses markdown language to create webpages. This blog uses mkdocs for documentation and organising my notes. 
>Learn more about mkdocs [here](https://www.mkdocs.org/)

## Getting started with MkDocs

>MkDocs official [getting started](https://www.mkdocs.org/getting-started/) page

------------
>**Note -** Before starting any python project, it is a best practice to create a virtual environment and work with that virtual environment to better manage all dependencies. [Read more](https://flask.palletsprojects.com/en/2.2.x/installation/#virtual-environments)

------------
Create and activate virtual env -
```batch
> mkdir myproject
> cd myproject
> py -3 -m venv venv
> venv\Scripts\activate
```

Install command -
```batch
(venv) C:\Projects\myprojects> pip install mkdocs
```

## $ `mkdocs new`

Create a new mkdocs project -
```batch
(venv) C:\Projects\myprojects> mkdocs new .
```

Alternatively, if you want to create a new project in a seperate directory, use this command -
```batch
(venv) C:\Projects> mkdocs new myprojects
``` 

## $ `mkdocs serve`

This command is used to host the static site created by mkdocs locally. 

```batch
(venv) C:\Projects\myprojects> mkdocs serve
```

A successful execution of this command gives output something like this -

```
INFO     -  Building documentation...
INFO     -  Cleaning site directory
INFO     -  Documentation built in 0.95 seconds
INFO     -  [03:56:37] Watching paths for changes: 'docs', 'mkdocs.yml'
INFO     -  [03:56:37] Serving on http://127.0.0.1:8000/
```

>**Note -** This command execution looks for `docs/` directory and a `mkdocs.yml` configuration file where the command is run.

## $ `mkdocs build`

This command build your static site inside `site\` directory. Example - `C:\Projects\myprojects\site\`. For more details [click here](https://www.mkdocs.org/getting-started/#building-the-site)

```batch
(venv) C:\Projects\myprojects> mkdocs build
```

**Note:** If you're using source code control such as `git` you probably don't want to check your documentation builds into the repository. Add a line containing `site/` to your `.gitignore` file.

```
echo "site/" >> .gitignore
```

## $ `mkdocs gh-deploy`

This command is used to deploy your mkdocs documentation on github pages. 

```batch
(venv) C:\Projects\myprojects> mkdocs serve
```

## What happens internally when gh-deploy is run?
-------------------------------------------------
\> `mkdocs gh-deploy`

MkDocs build your static site and push its content to gh-pages branch of the repo. Let's take a close look at the output of this command

>**Note:** For below output, mkdocs project is located in `E:\Code_Projects\Git Repos\CS-Notes\` directory

```linenums="1" hl_lines="2 5 14 15 17 18"
INFO     -  Cleaning site directory
INFO     -  Building documentation to directory: E:\Code_Projects\Git Repos\CS-Notes\site
INFO     -  Documentation built in 1.11 seconds
WARNING  -  Version check skipped: No version specified in previous deployment.
INFO     -  Copying 'E:\Code_Projects\Git Repos\CS-Notes\site' to 'gh-pages' branch and pushing to GitHub.
Enumerating objects: 65, done.
Counting objects: 100% (65/65), done.
Delta compression using up to 4 threads
Compressing objects: 100% (58/58), done.
Writing objects: 100% (65/65), 504.09 KiB | 1.40 MiB/s, done.
Total 65 (delta 7), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (7/7), done.
remote:
remote: Create a pull request for 'gh-pages' on GitHub by visiting:
remote:      https://github.com/nkitanand/CS-Notes/pull/new/gh-pages
remote:
To github.com:nkitanand/CS-Notes.git
 * [new branch]      gh-pages -> gh-pages
INFO     -  Your documentation should shortly be available at: https://nkitanand.github.io/CS-Notes/
```

- See *Line 2* - Your static site is being built into `site\` directory
- See *Line 5* - content of `site\` directory is copied to gh-pages branch of your local system
- See *Line 17-18* - since gh-pages is not yet created in our github repo (because `gh-deploy` is being run for the first time), this branch will get created automatically by this command in the github repo as well. 

>Note: If it is being run for the first time then gh-pages branch will be created by this command internally

## Deploying to GitHub Pages
----------------------------

### Manual deployment

Use the command [`gh-deploy`](/#mkdocs-gh-deploy) to manually deploy your changes to github pages. 

As a best practice, follow these 3 steps before making new changes -

1. Make changes to your local repo and verify changes using [`serve`](/#mkdocs-serve) command
2. Commit your changes and push it to your `main` or `master` branch of GitHub
3. Now, run [`gh-deploy`](/#mkdocs-gh-deploy) command in your local system to deploy changes to github pages.

### Automatic deployment

We can use GitHub Actions for automatically deploying changes to GitHub pages whenever a new commit is pushed to either the `master` or `main` branches.

To automate follow these [steps](https://squidfunk.github.io/mkdocs-material/publishing-your-site/)

#### Publishing your site

The great thing about hosting project documentation in a `git` repository is
the ability to deploy it automatically when new changes are pushed. MkDocs
makes this ridiculously simple.

#### GitHub Pages

If you're already hosting your code on GitHub, [GitHub Pages] is certainly
the most convenient way to publish your project documentation. It's free of
charge and pretty easy to set up.

  [GitHub Pages]: https://pages.github.com/

#### with GitHub Actions

Using [GitHub Actions] you can automate the deployment of your project
documentation. At the root of your repository, create a new GitHub Actions
workflow, e.g. `.github/workflows/ci.yml`, and copy and paste the following
contents:

=== "Material for MkDocs"

    ``` yaml
    name: ci # (1)!
    on:
      push:
        branches:
          - master # (2)!
          - main
    permissions:
      contents: write
    jobs:
      deploy:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v3
          - uses: actions/setup-python@v4
            with:
              python-version: 3.x
          - run: pip install mkdocs-material # (3)!
          - run: mkdocs gh-deploy --force
    ```

>Note: <br>
>1. `name:` - You can change the name (**ci** in this example) to your liking. <br>
>2. `branches:` - At some point, GitHub renamed `master` to `main`. If your default branch is named `master`, you can safely remove `main`, vice versa.<br>
>3. `run: pip install mkdocs-material` - This is the place to install further [MkDocs plugins] or Markdown extensions with `pip` to be used during the build:<br>
        ``` sh
        pip install \
          mkdocs-material \
          mkdocs-awesome-pages-plugin \
          ...
        ```

Now, when a new commit is pushed to either the `master` or `main` branches,
the static site is automatically built and deployed. Push your changes to see
the workflow in action.

If the GitHub Page doesn't show up after a few minutes, go to the settings of
your repository and ensure that the [publishing source branch] for your GitHub
Page is set to `gh-pages`.

Your documentation should shortly appear at `<username>.github.io/<repository>`.

  [GitHub Actions]: https://github.com/features/actions
  [MkDocs plugins]: https://github.com/mkdocs/mkdocs/wiki/MkDocs-Plugins
  [personal access token]: https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token
  [GitHub secrets]: https://docs.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets
  [publishing source branch]: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site