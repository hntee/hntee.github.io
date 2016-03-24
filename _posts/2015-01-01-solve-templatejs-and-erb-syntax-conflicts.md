---
layout: post
title: 解决 jq.template.js 与 erb 渲染 <%= %> 时的冲突 
date: 2014-05-17 16:06:12
tags:
---

今天需要编辑一个用`jq.template.js`渲染的html文件，可是当把这个文件放在rails的view中时，产生了一个解析的冲突。

<!-- more -->

原因是`jq.template.js`中template和erb的一样，都是`<%= %>`，当erb先解析时，`<%= %>`中是它不认识的数据，因此就报错了。

解决方法就是把`jq.template.js`的模板格式改掉，使之不与erb冲突。

寻找答案的过程也不是那么顺利，一开始并不了解JavaScript是如何渲染模板的，用了一段时间也没找到如何设置。

后来搜索到`jq.template.js`的源码看了一下，其中重点是这一段。

```javascript
// Simple JavaScript Templating
// John Resig - http://ejohn.org/ - MIT Licensed
(function(){
  var cache = {};
 
  this.tmpl = function tmpl(str, data){
    // Figure out if we're getting a template, or if we need to
    // load the template - and be sure to cache the result.
    var fn = !/\W/.test(str) ?
      cache[str] = cache[str] ||
        tmpl(document.getElementById(str).innerHTML) :
     
      // Generate a reusable function that will serve as a template
      // generator (and which will be cached).
      new Function("obj",
        "var p=[],print=function(){p.push.apply(p,arguments);};" +
       
        // Introduce the data as local variables using with(){}
        "with(obj){p.push('" +
       
        // Convert the template into pure JavaScript
        str
          .replace(/[\r\t\n]/g, " ")
          .split("<%").join("\t")
          .replace(/((^|%>)[^\t]*)'/g, "$1\r")
          .replace(/\t=(.*?)%>/g, "',$1,'")
          .split("\t").join("');")
          .split("%>").join("p.push('")
          .split("\r").join("\\'")
      + "');}return p.join('');");
   
    // Provide some basic currying to the user
    return data ? fn( data ) : fn;
  };
})();
```

接着把`<%`和`%>`分别改成<code>&#123;%</code>和<code>%&#125;</code>，再把 erb 中相应的内容也改掉就完成了。


