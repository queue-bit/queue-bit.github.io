---
title:  "md2confluence"
intro: "I created a set of Ruby libraries to convert markdown to Confluence and upload it."
description: "A set of Ruby libraries to convert markdown to Confluence and upload it."
tags: "ruby, markdown, confluence, atlassian"
date: "2022-11-05"
updated: "2022-11-17"
---

### Requirements

**Purpose**

I need to be able to convert GitHub Flavoured Markdown to Confluence markup and automatically upload it to Atlassian Confluence, every opensource tool I've tested for this breaks with mixed nested lists.

**Intro**
|||
|-|-|
| **For** | Myself |
| **Who**| Needs to upload markdown documents to Confluence|
| **The** | md2confluence tool converts markdown to Confluence markup and automatically uploads it|
| **That** | can be integrated with other programs |
| **Unlike**| Most existing opensource solutions|
| **This Product** |handles mixed nested lists without breaking.|

**Who is it for?**

*md2confluence* is primarily for myself as I prefer writing in markdown than wysiwyg editors or Confluence markup.

**Background**

I needed to upload a mass of markdown files to Confluence but every tool I tested would break with my mixed nested lists (ordered within unordered, etc) so I set to build it for myself.

**Market Assumptions**

- I will be the only person using *md2confluence*.

**Market Opportunities**

- Not applicable as this is a personal project.

**Goals**

- Create a markdown to Confluence converter
- Use the Confluence API to upload the content
- Keep the content file/path structure from the markdown files when creating pages on Confluence

**Features / Functionality**

- Core Elements
  - Library:
    - Convert markdown to Confluence markup
      - Must support uploading images as attachments and having them show in the Confluence page appropriately
    - Confluence API
  - Examples:
    - Convert single page
    - Convert directory tree
    - Delete directory tree from Confluence
- Look and Feel
  - *md2confluence* should be a set of two libraries, one to handle the markdown conversion and the other to handle the Confluence API.
  - These libraries can be included in other projects or can be wrapped with a simple program to convert one or many files.

**Release Criteria**

- Library can convert markdown test corpus to Confluence markup
- Library can connect to Confluence, upload, and delete pages
- Examples of using the libraries to:
  - Process and upload a single file
  - Process and upload a directory tree
  - Delete a tree of pages from Confluence


**Timeline & Constraints**

- No budget or dependencies, I am the only resource.
- Can only be worked on over weekends and when time allows

---

### Current Release Details

The repo: [md2confluence](https://github.com/queue-bit/md2confluence)

I opted to write this in Ruby for practice. The core functionality is built into libraries for future re-use, several examples are provided in the repo to illustrate how to use these libraries to process a single file, a directory tree, and how to delete pages from Confluence.

Please be sure to read and understand the [license](https://github.com/queue-bit/md2confluence/blob/main/LICENSE) before using this.

#### Libraries

The solution contains two libraries

##### confluence-client.rb

In the Repo: [/lib/confluence-client/confluence-client.rb](https://github.com/queue-bit/md2confluence/tree/main/lib/confluence-client)

This library handles the Confluence API for things like:

1. Creating a new page
2. Getting an existing page by ID or Parameters
3. Updating an existing page
4. Getting attachment metadata
5. Deleting a page or attachment
6. Setting a mime-type for a file upload (automatically when possible)
7. Adding an attachment to a Confluence page
8. Updating an attachment on a Confluence page

##### md2confluence.rb

In the Repo: [/lib/md2confluence/md2confluence.rb](https://github.com/queue-bit/md2confluence/blob/main/lib/md2confluence/md2confluence.rb)

I won't call out everything this library does in detail, but there's a few things to note:

1. Handles:
   - Font styling (italic, bold)
   - Headers
   - Code blocks (language definition of the code block not supported)
   - Inline code
   - Frontmatter (see [Frontmatter](#frontmatter))
   - Horizontal rules
   - Links (see [File and Image Links](#file-and-image-links))
   - [Mixed / nested lists](#how-lists-are-handled)
   - Tables (lists within tables not supported)
   - Certain macros (defined in the supported-macros.config file)
2. Because matching is done by Regex, the order of operations in the program is important. Moving statements around will likely break the parsing.

###### Frontmatter

At the start of the document you can define the following metadata, none of the fields are required.

This allows you to set the Confluence `space`, `parent` page, document `title`, and whether or not a table of contents (`toc`) will be included for each markdown file.

Note: `version` is defined in the frontmatter, this isn't used for Confluence versioning, if defined it will show at the top of the Confluence document in a panel. This is included for displaying a document version in policy controlled environments.

```yaml
---
space: "COMPANY"
parent: "Procedures"
title: "Writing Procedures Procedure"
version: "1.0.1"
toc: "true"
tags: "Each word here is a tag/label"
---

# Your markdown here
```


###### File and Image Links

When there's a link in the markdown, the program checks if it's to a typical URI protocol (i.e. https, http, rss, ftp, sftp), file type (i.e. html, htm, asp, aspx, cf, php), or anchor link (i.e. starts with `#`) if it's none of these it's assumed to be a file.

The link is then parsed for the filename and the program checks if the file exists. If the file exists, it's added to the files to be uploaded to Confluence as an attachment and the link in the markdown is converted to a Confluence attachment link.


###### How lists are handled

This was a challenge and deserves to be called out. 

In markdown lists are easily created and can be formatted like:

```md
- first primary item
    - first subitem
  - second subitem
- second primary item
    1. a numbered subitem
        1. a second numbered subitem
```

The problem comes in with how permissive markdown can be with regards to indenting, notice that `second subitem` isn't indented as much as `first subitem`? In most rendering tools they'll show up at the same level (correctly) but most parsers that output for Confluence will break and do unexpected things with the content.

To handle this, I came up with the following:

1. Get the number of characters used in the `indent` then see if it exists in an array created to track it  `li_levels`
2. If it doesn't exist, check if the `indent` is > the last item in the `li_levels` array
   - If yes: Push this item onto the array and get the array index for that value
   - If no: Find the closest match in the array and get the array index for that value
3. If it does exist, get the index for that `indent` value
4. If indent for the line is == 1 then clear the array and start over (add `1` once cleared)     

In testing against my corpus I found this worked extremely well, you can see the [code here](https://github.com/queue-bit/md2confluence/blob/c7e335a36cb06a94996802047073f18d801c9c1c/lib/md2confluence/md2confluence.rb#L198).

#### Examples

Three usage examples are provided, you'll need to adjust the Confluence API configuration in the files.

##### example-single-page.rb

Converts a single page to Confluence markup and uploads it. 

[Link to file](https://github.com/queue-bit/md2confluence/blob/main/example-single-page.rb)

##### example-convert-directory.rb

Converts an entire directory to Confluence markup and uploads it. The directory tree will be maintained (that is, if a file was in /docs/example.md it will be at /docs/example in Confluence). 

[Link to file](https://github.com/queue-bit/md2confluence/blob/main/example-convert-directory.rb)

##### example-convert-directory-delete.rb

This will delete the files that were created with example-convert-directory.rb. 

[Link to file](https://github.com/queue-bit/md2confluence/blob/main/example-convert-directory-delete.rb)
