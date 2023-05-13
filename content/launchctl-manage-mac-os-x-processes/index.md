---
title: "launchctl — manage Mac OS X processes"
description: "Use launchctl to stop a Mac OS X process that’s running in the background."
date: "2017-09-12T09:43:18.438Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/launchctl-manage-mac-os-x-processes-f679b4b3a675
redirect_from:
  - /launchctl-manage-mac-os-x-processes-f679b4b3a675
---

Use `launchctl` to stop a Mac OS X process that’s running in the background.

```
$ sudo launchctl list | grep -i foo
list of results
31415   0       com.foo.the
27182   0       quick.brown.fox
161     0       jumps.over.lazy.dog
$ sudo launchctl remove com.foo.the
```

The end.
