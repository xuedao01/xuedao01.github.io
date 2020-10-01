---
title: npm设置代理
date: 2020-10-01 08:10:49
tags: npm
---

**设置代理**

```
npm config set proxy=http://127.0.0.1:7890
npm config set https-proxy http://127.0.0.1:7890
```

<!--more-->

**取消代理**

```
npm config delete proxy
npm config delete https-proxy
```

参考来源：https://www.cnblogs.com/luomingsong/p/10723503.html

