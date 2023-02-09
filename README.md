Welcome to the source code repository for [The AWS Step Functions Workshop](https://catalog.workshops.aws/stepfunctions/en-US)!


## Repository structure

```bash
.
├── contentspec.yaml                  <-- Specifies the version of the content
├── README.md                         <-- This instructions file
├── static                            <-- Directory for static assets to be hosted alongside the workshop (ie. images, scripts, documents, etc) 
└── content                           <-- Directory for workshop content markdown
    └── index.en.md                   <-- At the root of each directory, there must be at least one markdown file
    └── index.pt.md                   <-- localized Portuguese content  
    └── index.es.md                   <-- localized Spanish content  
    └── introduction                  <-- Directory for workshop content markdown
        └── index.en.md               <-- Markdown file that would be rendered
        └── index.pt.md                   <-- localized Portuguese content  
        └── index.es.md                   <-- localized Spanish content  

```

## What's Included

This project contains the following folders:
* `static`: This folder contains static assets to be hosted alongside the workshop (ie. images, scripts, documents, etc) 
* `content`: This is the core workshop folder. This is generated as HTML and hosted for presentation for customers.

## How to create content

Under the `content` folder, Each folder requires at least one `index.<lang>.md` file. The file will have a header

```aidl
+++
title = "Welcome to The AWS Step Functions Workshop!"
weight = 0
+++
```

The title will be the title on navigation panel on the left. The weight determines the order the page appears in the navigation panel.

## Local development

The root directory of this project contains the *preview_build* utility for MacOs and the *preview_build.exe* utility for Windows. This utility allows you to perform local development by viewing the workshop in a local web server. You run the utility on your computer to perform local builds. When you update content, the webpages will automatically reload so you can view your changes. This makes content authoring and editing easier and faster. 




