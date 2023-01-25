# How to use the Varaiable in HTML Style?

> Codebase
```
<script>
  let size = 100;
</script>

<div style='--width_size:{size};'></div>

<style>
  div {
    width : calc( var(--width_size) * 1px );
  }
</style>
```

This works well for me.
:-)