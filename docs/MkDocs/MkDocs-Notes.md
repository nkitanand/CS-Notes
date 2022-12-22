# MkDocs

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

## What happens internally when gh-deploy is run
-----------------------------------------------
\> `mkdocs gh-deploy`

MkDocs build your static site and push its content to gh-pages branch of the repo

>Note: If it is being run for the first time then gh-pages branch will be created by this command internally

