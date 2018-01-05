---
layout:     post
title:      "WebStorm tips"
subtitle:   "WebStorm tips"
date:       2016-03-11 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# Shortcuts

## Selection

Multiselection: 

`Ctrl + Cmd + G`

## Move

Popup list of the recently visited files. Choose the desired file and press Enter to open it:

 `Ctrl + E  `

Last cursor position:

 `Ctrl + Alt + Left-Arrow (or Cmd + Alt + Left-Arrow on Mac) `

Last Edit Location:

`Ctrl + Shift + Bakcspace (or Cmd + Alt + Backspace on Mac)`

List recently viewed files:

`Ctrl + E`

List recently edited files:

`Ctrl + Shift + E`



# Auto complete

Instead of write

	<md-content></md-content>

 try	`md-content` then press TAB, you will get by magic the same completed tag.

Advanced usage is `md-content#content`, Then TAB, you will get

	<md-content id="content"></md-content>

And with `md-content.content` you can get 

    <md-content class="content"></md-content>




## Webstorm debug setting

### For ['React-boilerplate'](https://github.com/react-boilerplate/react-boilerplate/blob/master/docs/general/debugging.md#debugging-with-webStorm)

1. [Install JetBrain Chrome Extension](https://chrome.google.com/webstore/detail/jetbrains-ide-support/hmhgeddbohgjknpmjagkdomcpobmllji)
2. Change WebPack devtool config to `source-map` [(This line)](https://github.com/react-boilerplate/react-boilerplate/blob/56eb5a0ec4aa691169ef427f3a0122fde5a5aa24/internals/webpack/webpack.dev.babel.js#L65)
3. Run web server (`npm run start`)
4. Create Run Configuration (Run > Edit Configurations) : Add new `JavaScript Debug`
   1. URL:   `http://localhost:3000`
   2. Map your `root` directory (`Remote URLs of local files`) with `webpack://.` 
5. ​Right click JetBrain plugin icon, click "Inspect In WebStorm"

# 