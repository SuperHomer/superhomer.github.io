---
layout: post
title:  "Clean npm packages in your project"
date:   2022-06-08 10:05:00 +0100
categories: clean npm package
---

When web projects get bigger, you can have many npm packages installed. There are some used, some outdated and some not used at all. It's very important to have a clean package repository, because you can have some undesirable situation. For example, you may find yourself in a situation where you want to update some packages because of some critical vulnerabilities. It can happend that you cannot simply update packages because of dependencies and/or requirements on package you never heard of and you don't even know if they are used.

In this post, some technics to have a clean npm packages repository will be explained.

## depcheck
>Depcheck is a tool for analyzing the dependencies in a project to see: how each dependency is used, which dependencies are useless, and which dependencies are missing from `package.json`.

```
$ npm install -g depcheck
$ depcheck

Unused dependencies
* ...
Unused devDependencies
* ...
Missing dependencies
* ...
```


## npm-check
> Check for outdated, incorrect, and unused dependencies.

```
$ npm install -g npm-check
$ npm-check
```
![<img src="https://cloud.githubusercontent.com/assets/51505/9569917/96947fea-4f48-11e5-9783-2d78077256f2.png">](https://cloud.githubusercontent.com/assets/51505/9569917/96947fea-4f48-11e5-9783-2d78077256f2.png)

## cost-of-modules
> Find out which of your dependencies is slowing you down
This package will hep you find out packages which are very big and/or have multiple dependecies.

```
$ npm install -g cost-of-modules
$ cost-of-modules
```

![<img src="https://raw.githubusercontent.com/siddharthkp/cost-of-modules/master/screenshot.jpg">](https://raw.githubusercontent.com/siddharthkp/cost-of-modules/master/screenshot.jpg)

Another way to have the cost of each package, is directly using a vs code extension: [import cost](https://marketplace.visualstudio.com/items?itemName=wix.vscode-import-cost)

![<img src="https://citw.dev/_next/image?url=%2fposts%2fimport-cost%2f1quov3TFpgG2ur7myCLGtsA.gif&w=1080&q=75">](https://citw.dev/_next/image?url=%2fposts%2fimport-cost%2f1quov3TFpgG2ur7myCLGtsA.gif&w=1080&q=75)


## ls
> List installed packages
By specifying a package name, you will see all dependencies and version for the package.

```
$ npm ls <package_name>
```