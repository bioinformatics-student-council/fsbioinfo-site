# Bioinformatics Student Council Website

![GitHub Workflow Status (with event)](https://img.shields.io/github/actions/workflow/status/bioinformatics-student-council/fsbioinfo-site/.github/workflows/hugo.yaml)
[![gohugo](https://img.shields.io/badge/Made_with-Hugo-blue)](https://gohugo.io/)
[![tailwindcss](https://img.shields.io/badge/Made_with-Tailwind_CSS-blue)](https://tailwindcss.com/)
![GitHub Repo stars](https://img.shields.io/github/stars/bioinformatics-student-council/fsbioinfo-site)


Website of the bioinformatics student council ("Fachschaft Bioinformatik") at Goethe University Frankfurt.

## How to contribute

First of all, thank you so much for reading this! Since this website is run by students in their spare time, we very much appreciate any help we can get. If you see anything that you would like to improve or that needs to be updated, feel free to create an issue or a pull request.

## Local setup

To setup the website locally for development purposes, first [install Hugo](https://gohugo.io/installation/) and clone the repository:
```bash
git clone https://github.com/bioinformatics-student-council/fsbioinfo-site.git --recursive
```
Note that to download the theme that is used for the website, `--recursive` has to be provided.

After installing Hugo and cloning the repository, we can now setup our theme. Because custom layouts are used, we need to adjust the theme config:

```bash
cd fsbioinfo-site/themes/tailwind

# update which files are taken into considerations when building css
awk 'NR==6 {sub(/$/, ","); print; print "    \"../../layouts/**/*.html\""; next} 1' tailwind.config.js > tmp && mv tmp tailwind.config.js

# update theme package to serve our site, not the example site
awk '{gsub(/exampleSite/, "../.."); gsub(" --themesDir=../..", ""); print}' package.json > temp && mv temp package.json

# install theme package
npm install
```

All done! You can now preview the page with automatic updates by running:
```bash
npm run dev
```