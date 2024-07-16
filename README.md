# Example

![](./example.gif)
将你自己的组件或内容放入 `Simulate3D` 组件中即可！  
然后就可以通过鼠标对它拖拽、旋转和缩放了！

# How to use

```html
<template>
  <Simulate3D>
    <div class="dv">你自己的组件或内容</div>
  </Simulate3D>
</template>

<script>
  import Simulate3D from "simulate3d/src/Simulate3D.vue";
  export default {
    components: {
      Simulate3D,
    },
  };
</script>

<style>
  .dv {
    width: 400px;
    height: 400px;
    background-color: goldenrod;
  }
</style>
```
