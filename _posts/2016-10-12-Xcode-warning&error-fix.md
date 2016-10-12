---
layout: page
title: Xcode 警告和报错的修复 tips
---

### Multiple build commands for output file 

出现这个 warning 一般是重复引用或者重复关联了，对应的 Target -> Build Phases  搜索对应的关键字，去掉多余的即可