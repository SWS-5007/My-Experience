# React, Browser - How to disable auto fill button on Safari Browser?

> Note

I experienced cors error when implement image download by React.

How to fix:

You need to add "no-cache" at the end of the image url and cors error will be disappeared.
When browser downloads images, it first checks cache and in some cases, it caused cors error.
"no-cache" makes browser download image not from cache, so error will be disappeared.

This works well for me.
:-)
