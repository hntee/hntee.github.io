---
layout: post
title: "Sublime Text 2: Set Tab Size for Certain File Type"
date: 2014-04-10 18:37:56 +0800
comments: true
categories: 
---
Sometimes I need to set different tab size for different file type, say,
tab size of Python would be 4 and tab size of Ruby would be 2.

After some search, I found a way to do this.

Go to `Preferences -> Settings More -> Syntax Specific User` and edit the
file as follows.

```json
{ 
  "tab_size" : 2,
  "translate_tabs_to_spaces" : true
}
```

Now it will be good!

