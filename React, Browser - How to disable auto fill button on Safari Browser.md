# React, Browser - How to disable auto fill button on Safari Browser?

> Codebase

You just need to add this css in your code.

```
input::-webkit-contacts-auto-fill-button {
  visibility: hidden;
  display: none !important;
  pointer-events: none;
  position: absolute;
  right: 0;
}
```

This works well for me.
:-)
