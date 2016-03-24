---
layout: post
title: "CSS Pseudo Elements"
date: 2014-04-19 19:15:29 +0800
comments: true
categories: 
---

I just watched [a speech][1] by [Chris Coyier][2] about CSS pseudo elements. It contains a lot of insteresting tricks that I have never thought about, so I took down some notes for future reference.

These methods are mostly in a `:before` or a `:after` pseudo class. With these two, we can add content without configuring the html file.

<!-- more -->

### A quotation mark before and after a blockquote
[DEMO][3]

```html
<blockquote>
  <p>First paragraph. First paragraph. First paragraph. First paragraph. First paragraph. First paragraph. First paragraph. </p>
  <p>Second paragraph. Second paragraph. Second paragraph. Second paragraph. Second paragraph. Second paragraph.</p>
</blockquote>
```

```css
blockquote {
  position: relative;
}
blockquote p:first-child:before {
  content: '\201c'; /* left quotation mark */
  color: blue;
  position: absolute;
  top: 0px;
  left: -10px;
}
blockquote p:last-child:after {
  content: '\201d';  /* right quotation mark */
  color: blue;
}
```

In order not to influence contents in the `blockquote`, the left quotation mark is placed outside the block by `position: absolute`.

### Multiple backgrounds
[DEMO][4]

Since an html tag can have both `:before` and `:after` pseudo classes, it can have up to three backgrounds by just modifying CSS.

Here is how:

```html
<div id="silverback"></div>
```

```css
#silverback {
  position: relative;
  z-index: 1;
  padding: 120px 200px 50px;
  background: #d3ff99 url(http://silverbackapp.com/images/backgrounds/body.gif) 110% 0 repeat-x;
}

#silverback:before,
#silverback:after {
  position: absolute;
  z-index: -1;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  padding-top: 100px;
}

#silverback:before {
  content: "";
  background: transparent url(http://silverbackapp.com/images/backgrounds/vines-mid.png) 300% 0 repeat-x;
}

#silverback:after {
  content: "";
  background: transparent url(http://silverbackapp.com/images/backgrounds/vines-front.png) 70% 0 repeat-x;
}
```

Actually, the `content` can also include an image, like `content: url(image.png)`.
`padding` and `text-align` take effect too. The initial post about this method is created by [Nicolas Gallagher][5].

Referrence: 
 - [A Whole Bunch of Amazing Stuff Pseudo Elements Can Do][6]
 - [Multiple Backgrounds and Borders with CSS 2.1][7]

[1]: http://wordpress.tv/2011/09/09/chris-coyier-css-pseudo-elements-for-fun-and-profit/
[2]: http://chriscoyier.net/‎
[3]: http://jsbin.com/camor/1/edit
[4]: http://jsbin.com/bakif/2/edit
[5]: http://nicolasgallagher.com/
[6]: http://css-tricks.com/pseudo-element-roundup/
[7]: http://nicolasgallagher.com/multiple-backgrounds-and-borders-with-css2/
