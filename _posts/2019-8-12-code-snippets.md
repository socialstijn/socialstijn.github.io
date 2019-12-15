---
layout: post
title:  Code snippets in a blog post
categories: [HTML,Code]
---

This post demonstrate the use of code snippets in the theme. The code snippets are powered by [Pygments](http://pygments.org/) and the code theme that is been used in Reverie is called [Draula](https://draculatheme.com/).

This is a raw snippet:

```
hello world
123
This is a text snippet
```

This is a PHP snippet:

```php
<?php
    echo 'Hello, World!';
?>
```

This is a JavaScript snippet:

```js
const add = (a, b) => a + b
const minus = (a, b) => a - b

console.log(add(100,200))  // 300
console.log(minus(100,200))  // -100
```

This is a Bash snippet:

```bash
#!/bin/bash

echo How old are you?

read age

if [ "$age" -gt 20 ]
then
    echo You can drink.
else
    echo You are too young to drink.
fi
```
