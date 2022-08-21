---
title: "Create GitHub Page with Hugo"
date: 2022-08-17
tags: ["github", "hugo"]
draft: false
---

## intro

If you want to have your personal website without putting too much effort in it GitHub Pages is your way to go. You can simply push the index.html to your public folder on the main branch and you have your website. But there is a little problem, it will be a very basic one so you would have to code all the styling from scratch, not to mention logic. Don't worry **Hugo** got you covered, you can install themes and setup automatic build wih github workflows, let's see how to set it up...

---

## quick step-by-step tutorial

1. create github repo \<USERNAME\>.github.io
   
2. In `Settings > Pages` set:
   - Source to `Deploy from a branch`
   - Branch to `gh-pages`

3. Create GitHub workflow configuration for [Hugo](https://gohugo.io/hosting-and-deployment/hosting-on-github/)
   - create file `.github/workflows/gh-pages.yml` and open it
   - paste [this](https://gohugo.io/hosting-and-deployment/hosting-on-github/#build-hugo-with-github-action) inside
   - save the file
  
4. Add a [theme](https://themes.gohugo.io/)
   - example installation for [Minimal](https://themes.gohugo.io/themes/minimal/)
  ```
  git submodule add https://github.com/calintat/minimal.git themes/minimal
  git submodule init
  git submodule update
  git submodule update --remote themes/minimal
  ```
5. From `./themes/<theme-name>/exampleSite` copy folder `content` and file `config.toml` to your root folder
6. Update newly copied file `config.toml`:
    - change `baseURL` to `https://<YOUR-REPO-NAME>/` in my case it is `https://antooni.github.io/`

7. Commit changes and push them to master
8. Visit your website!
   
Now you can edit certain files, add, remove, anything you like as long as you don't break things. I highly recommend doing the next section so you will be able to create your local build environment and see the changes before pushing them to GitHub.

---

## install Hugo and run it locally

1. Install Hugo for your operating system [link](https://gohugo.io/getting-started/installing)

2. Inside root folder of your repo run `hugo server -D`

It should print the local address of your webpage, in my case it is [http://localhost:1313](http://localhost:1313). The changes you made to the files are being automatically built so you can easily tinker with it. Enjoy and let me know if my tutorial helped you, preferably via email.

---

*when clonning new repo from GH remeber to 
```
   git submodule init
   git submodule update
   git submodule update --remote themes/minimal
```
