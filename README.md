# Aws-workshop-template

## Powerpoint template

The images in the Introduction section were created from a Powerpoint at [this workdocs location](https://amazon.awsapps.com/workdocs/index.html#/document/8d80b53c20323c14316a722c047e8ae03136295b87f19d6839498a04568d5066).


## Repo structure

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
title = "AWS Workshop Template"
weight = 0
+++
```

The title will be the title on navigation panel on the left. The weight determines the order the page appears in the navigation panel.

## Local development

The local development preview utility allows you to view changes to your content without having to push changes to the repository. You run the utility on your computer to perform local builds. When you update content, the webpages will automatically reload so you can view your changes. This makes content authoring and editing easier and faster. This project contains the *preview_build* utility for MacOs in the root directory.

[Learn more about local development](https://studio.us-east-1.prod.workshops.aws/preview/580d5100-7d5d-4475-a08a-869479cdb428/builds/57a6cd8c-95a2-4fae-b2e7-03ee4935e9f4/en-US/authoring-a-workshop/local-development).