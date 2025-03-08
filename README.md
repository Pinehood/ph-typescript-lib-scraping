## Introduction

Shared library for "ph-portals" and "ph-configurable-web-scraper" projects.

## Installations

- [Node.js](https://nodejs.org/en/download/) (version >= 18.10.0)
- [Visual Studio Code](https://code.visualstudio.com/download) (and "Prettier - Code formatter" extension)

## Setup

1. Prerequisites:

- must have installed tools from the "Installations" section
- must have checked out / cloned source code from this repository

2. Open up the cloned repository/project/folder and run following commands in the given order, one by one:

   ```
   npm install
   npm run build
   ```

3. Both of the above commands should have completed successfully, and should have not caused any "package.json" or "package-lock.json" changes.

## Example

A simple, working JSON configuration object that can be used to scrape articles from Dnevno.hr news portal into a local JSON file.

```json
{
  "name": "Dnevno.hr News Portal",
  "base": "https://www.dnevno.hr",
  "favicon": "https://dnevno.hr/favicon.ico",
  "roots": [
    "https://www.dnevno.hr/category/vijesti",
    "https://www.dnevno.hr/category/sport",
    "https://www.dnevno.hr/category/magazin",
    "https://www.dnevno.hr/category/gospodarstvo-i-turizam",
    "https://www.dnevno.hr/category/planet-x",
    "https://www.dnevno.hr/category/zdravlje",
    "https://www.dnevno.hr/category/domovina",
    "https://www.dnevno.hr/category/vjera"
  ],
  "links": {
    "fetching": {
      "method": "GET"
    },
    "selector": "article.post a",
    "type": "html"
  },
  "remove": [
    "img",
    "iframe",
    "div.wpipa-container",
    "div.lwdgt-container",
    "p.lwdgt-logo",
    "center",
    "blockquote",
    "figure",
    "figcaption"
  ],
  "scrape": [
    { "property": "title", "selector": "h1" },
    { "property": "lead", "selector": "a.title" },
    {
      "property": "time",
      "selector": "time.date",
      "take": "first",
      "type": "text",
      "transfomers": [
        {
          "type": "split",
          "value": ",",
          "index": 1
        },
        {
          "type": "trim"
        }
      ]
    },
    {
      "property": "author",
      "selector": "span.author",
      "take": "first",
      "transformers": [
        {
          "type": "split",
          "value": "Autor:",
          "index": 1
        },
        {
          "type": "trim"
        }
      ]
    },
    {
      "remove": [
        "div.img-holder",
        "div.heading",
        "h1",
        "style",
        "div.info",
        "div.info-holder"
      ],
      "property": "content",
      "selector": "section.description",
      "type": "html"
    }
  ],
  "submit": {
    "type": "file",
    "destination": "./dnevno.json"
  }
}
```
