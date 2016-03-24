---
layout: post
title: "用python和wget来抓取中证市盈率数据"
date: 2014-03-12 11:50:00
tags: 
---

前段时间关注了一个ETF投资的人，大体思路是按照市盈率来对指定ETF进行买入和卖出操作。

不过此君一个月操作一次，且操作时的市盈率要他发布在博客的时候才知道。

投资不能这么依靠别人，所以应该自己抓数据过来分析。


经过寻找，发现在中证的网站上居然有各行业各股票每一天的市盈率数据。

本来想用模拟查询的方法取数据，还动用了wireshark，最后还是没有成功。

那就下载文件吧。下载来一看居然行业个股的市盈率、股息率全都有，真是天助我也。

可惜下载一次只是一天的数据。

不过发现他的文件命名十分有规律，都是按照`http://www.csindex.com.cn/sseportal/ps/zhs/hqjt/csi/syl/csi20140310.xls`这样格式的，其中开市的日期就有数据。

所以想到用python按照日期生成URL，再用wget先嗅探再下载。

###python代码：
```python
	import datetime

	base = datetime.datetime.today()

	numdays = 1500

	dateList = [ base - datetime.timedelta(days=x) for x in range(0,numdays) ]

	thefile = open('datesUrl.txt', 'w')

	for item in dateList:
	  thefile.write("%s%s%s\n" 
	  	% ('http://www.csindex.com.cn/sseportal/ps/zhs/hqjt/csi/syl/csi',
	  		item.strftime("%Y%m%d"),
	  		'.xls'))
```

*经过测试有数据的最早的时间是20110503。*

这时候就生成了`datesUrl.txt`，再用`wget`的`--spider`参数探测哪些是可用链接。

###bash代码：

```
#!/bin/bash

input=datesUrl.txt

while read line
do
    wget --spider $line && echo $line >> ok.txt
done < "$input"

```

此时可用的地址都生成到`ok.txt`中了。

再用`wget -i ok.txt`即可全部下载。

获得xls之后还要继续处理，留到下一篇再写。

