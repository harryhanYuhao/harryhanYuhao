---
date: '2025-04-12T12:06:23+01:00'
title: 'Deploy Hugo Blog site with Github Pages'
# weight: 1
tags: ["web", "blogging"]
showToc: true
TocOpen: false
hidemeta: false
comments: false
description: "Quick steps to create a blog with Github Pages, Hugo, and PaperMod. Prerequisite: simple command line, git."
# canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
#cover:
#    image: "<image path/url>" # image path/url
#    alt: "<alt text>" # alt text
#    caption: "<text>" # display caption under cover
#    relative: false # when using page bundles set this to true
#    hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/harryhanYuhao/harryhanYuhao/tree/main/hugo_site/content/posts"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

Blogging with Hugo, Papermod, and Github pages is easy. 
(Writing the articles, of course, is a different business). 
This is a short guide for how to create and maintain such a website.

To create a static blogging websites only requires
1. Create the HTML, CSS, Javascript files, which are downloaded by the browser uponing entering its domain name;
1. Obtain a domain name and host the files on a server connected to internect with this domain name.

[Hugo](https://gohugo.com) and [Papermod](https://github.com/adityatelange/hugo-PaperMod) can read the markdown files and produce stylish webpages. (That is the HTML, CSS, and Javascript files.)
Github pages is a free remote service hosting the file and provide the domain name.

These tools are used to create a static blog website.
The term static means the content of the website does not change with respect to user input. 
In fact, there may be no options for user inputs at all.
Most websites, however, are not static. 
The prime examples are social medias, which can show live contents based on user inputs.
Creating these websites, of course, are more complicated and requires a separate *backends*. (In comparison, all the files Hugo and Papermod created are *frontend*.)

## Creating the Website with Hugo

Hugo has an official [tutorial](https://gohugo.io/getting-started/quick-start/), so is [Papermod](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation).
Here is presented an adaptation.

After installing Hugo and Git, create a Hugo project
```bash
hugo new site NewWebsite --format yaml # replace NewWebsite with any name
```
Enter the new directory and install Papermod as an Module
```bash
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
```

Append the following line in `hugo.yaml` 
```
theme: ["PaperMod"]
```

Start the hugo testing server with 

```sh
hugo server -O  # -O flag will open the browser
```

The next command will create a markdown file of a specified format in directory `contents/posts/`.
Each blog articles are renderred from the contents and the struture of these markdown files.

```sh
hugo new content content/posts/my-first-post.md
```

Write the blog contents into this file. 
Delete `draft: true` line in the preamble of the file to make it visible.

### Styling 

Papermod takes care of the styling, and offers some [customisations](https://github.com/adityatelange/hugo-PaperMod/wiki/Features), which are doen by editing entries in the `hugo.yaml` file. 
Papermod presents an [example site](https://github.com/adityatelange/hugo-PaperMod/tree/exampleSite/).
The config file of this site is [here](https://github.com/harryhanYuhao/harryhanYuhao/blob/main/hugo_site/hugo.yaml).

Notably,

The contents on the homepage is presented via `params -> homeInfoParams`. 
```yaml
# hugo.yaml
params:
  homeInfoParams:
    Title: >
      Some mathematics, coding, and Literature

    Content: >
      👋 Welcome to Harry's blog pages.

      - This blog is made by [hugo](https://gohugo.io) and [papermod](https://github.com/adityatelange/hugo-PaperMod), and is deployed with Github Pages.
```

To show menu on the top right, uses `menu` directory
```yaml
menu:
  main:
    - name: Archive
      url: archives/
      weight: 10
    - name: Tags
      url: tags/
      weight: 10
    - name: Search
      url: search/
      weight: 10
```

Tag pages will work automatically.
For the archives, and search to work requires a little more work, documented here: [archives](https://github.com/adityatelange/hugo-PaperMod/wiki/Features#archives-layout), [searches](https://github.com/adityatelange/hugo-PaperMod/wiki/Features#search-page).

Basically, for archive one just need to create `content/archive.md` file and write to it
```
---
title: "Archive"
layout: "archives"
url: "/archives/"
summary: archives
---
```
For search, create `content/search.md` file and write to it
```
---
title: "Search" # in any language you want
layout: "search" # necessary for search
# url: "/archive"
# description: "Description for Search"
summary: "search"
placeholder: "placeholder text in search input box"
---
```
In addition, append `hugo.yaml` with 
```
outputs:
  home:
    - HTML
    - RSS
    - JSON # necessary for search
```

To hide particular pages from search, add 
```
searchHidden: true
```
on top of that page's markdown file.

## Hosting with Github Pages

Now the content is taken care of, we shall deploy it on Github.

Deploying an website manually is troublesome. 
The ideal and efficient workflow is that, whenever some changes is made in the blog, a quick command can be issued to automatically deploy our website.
This can be achieved by git and github actions. 

Github actions is a service for CI/CD (continuous integration/continuous deployment) workflow. 
A custom workflow can be designed to build an deploy our blog which will be triggerred automatically when the source files are pushed to github.
Github also offer Github Pages, a hosting service which integrated with github action nicely.
All of the above services are free.

If everything are set up correctly, each time changes are made in the blogging repository, the blogging website will be updated automatically. 
This is great productivity boost.

Let us set up the git and github actions.

### Some local modifications

Hugo create some auxiliary files which shall be ignored by git. 
Append the following lines into the `.gitignore` file.
```gitignore
# .gitignore
*.test
imports.*
dist/
public/
.DS_Store
```

The entry `baseURL` in `hugo.yaml` files needs to be set to

```
# hugo.yaml
baseURL: https://<username>.github.io/<repository-name>/
```

`<username>` is github username. `<repository-name>` is the github remote repo name, which are yet to be created.

The github actions are configured by a `yaml` files presented in `.github/workflows` directory. 

Create a `.github/workflows/hugo.yml` files, and write into it 
```
name: Build and depoly hugo to Github Pages

on:
  push:
    branches:
      - main  
  pull_request:
  workflow_dispatch:


permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-22.04
    concurrency:
      group: ${{ github.workflow }}-${{ github.ref }}
    steps:
      - uses: actions/checkout@v4
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: '0.145.0'
          extended: true

      - name: Build
        run: | 
          # cd hugo_site # this line is only neccesary if the site is not in the root directory
          hugo --minify

      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: public  # enter correct path


  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```
The file is [here](https://github.com/harryhanYuhao/harryhanYuhao/blob/main/.github/workflows/hugo.yml).

There are two things to take note. 
One is to place the correct hugo-version in `Setup Hugo` step.
The local hugo version can be found by
```
hugo version
```
Another is if the hugo site is not in the root directory of the git repository, you need to `cd` to correct directory and change the correct publish path in `Build` and `Upload Artifacts` steps.

Commit the changes to git. 
Now all local configurations are done.

### Setup Github Pages

Create a github repository. 
In the github repository. In `setting->code and automation -> pages`, change build and deployment source to Github Actions.
Pushing the local files to this github repository and everything shall work.

