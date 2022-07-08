---
title: First-try-in-Tampermonkey  
date: 2021-09-01 00:00:00  
tags:  
category: Life
---
A solution in Bilibili Directory Width  
Tampermonkey脚本，可点击该链接查看~  
[Bilibili视频选集标题显示完整](https://greasyfork.org/zh-CN/scripts/431806-bilibili%E8%A7%86%E9%A2%91%E9%80%89%E9%9B%86%E6%A0%87%E9%A2%98%E6%98%BE%E7%A4%BA%E5%AE%8C%E6%95%B4/code)

I start an open-sourced project in Tampermonkey, which sounds so cool, isn’t it?

I have been learning about Java in the atguigu, which is one of the most popular Java-Learning online courses in
Bilibili.
A problem struck me that the titles of hundreds of episodes are incomplete when viewing a separate video in collection.

I try to find an appropriate method for adopting the size of every title in their line.

So I write a script in Tampermonkey to solve this problem.

```javascript
// ==UserScript==
// @name         Bilibili视频选集标题显示完整
// @namespace    http://tampermonkey.net/

// @version      0.3
// @description  让标题显示完整~try to change Bilibili Directory Width!
// @author       HitLittleFox
// @license      AGPL-3.0
// @match        *://www.bilibili.com/*
// @grant        none
// ==/UserScript==

(function () {
    'use strict';
    var changeDirectoryWidth = document.querySelector(".multi-page .cur-list .list-box")
    changeDirectoryWidth.style.width = "fit-content"
})();
```