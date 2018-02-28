---
layout: post
title: Nodejs Association
date: 2018-02-13 10-34-30
categories: blog
---
# NodeJS Association on Windows

It seems that the Node.js x64 0.12.0 installation on Windows 8.1 adds the following file association with ".js" files to the registry:

HKEY_CLASSES_ROOT\Applications\node.exe\shell\open\command\
"@"=REG_SZ:"C:\Program Files\nodejs\node.exe" "%1"
Unfortunately, this does not allow passing arguments to the script:

C:\>test.js a b c
Arguments: []
Proposed fix
This is easily fixed by modifying the association and add "%*" like so:

HKEY_CLASSES_ROOT\Applications\node.exe\shell\open\command\
"@"=REG_SZ:"C:\Program Files\nodejs\node.exe" "%1" %*
Now if I run the same test, it works as expected:

C:\>test.js a b c
Arguments: ["a","b","c"]

https://github.com/nodejs/node-v0.x-archive/issues/9338