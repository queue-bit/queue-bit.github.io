---
title:  "Replace Jekyll on Github Pages"
intro: "If you're switching from Jekyll to something else on Github Pages, this worked for me."
description: "Switching from Jekyll to something else on GitHub Pages."
tags: "gh-pages, github-pages, pages, github, jekyll"
date: "2022-10-08"
---

### Edit Your Repo

I suggest you do these changes in a new branch, testing locally to make sure everything builds properly.

On your local:

1. Pull the repo
1. Update your content
   1. If you're switching to Hugo you can find a good write-up here: [https://blog.arkey.fr/2020/04/20/migrating-from-jekyll-to-hugo-deploying-with-github-pages/](https://blog.arkey.fr/2020/04/20/migrating-from-jekyll-to-hugo-deploying-with-github-pages/) 
   1. Remove all the Jekyll configuration files / cruft
   1. Add any configuration files you need for your new page builder
   1. Create a blank `.nojekyll` file in the root of the repo
1. Create a new file: `/.github/workflows/your-action-name.yaml` for your new workflow
   1. If you're switching to Hugo you can find information here: [https://github.com/marketplace/actions/hugo-setup](https://github.com/marketplace/actions/hugo-setup)
1. Commit your changes but don't merge yet

### Delete Jekyll

Once you have a branch that's been tested with your new page builder (Gatsby, Hugo, etc.) ready to go, you can go ahead and change settings on the Github end of things.

Note: When you're done this part your Github pages will be gone and you'll get 404's when visiting the site.

On Github:

1. Open the repo
1. Click `Settings`
1. Click `Pages`
1. Under `Build and deployment`, click the `Configure` button on the Jekyll entry
1. This will open a create action page, rename it to whatever you want, leave the body blank and click `Save` 
   - This will cause build errors, this will be fixed when you merge your new branch
1. Click `Actions`, delete all previous workflow runs
1. Merge your new branch - this should trigger a new build using the action you created in the [Edit Your Repo](#edit-your-repo) step

### Environment Protection Rules Error

If you get a `Branch "main" is not allowed to deploy to github-pages due to environment protection rules` error, this is easily fixed.

On Github:

1. Open the repo
1. Click `Settings`
1. Click `Environments`
1. Under `Deployment Branches`, make sure your branch is "allowed"