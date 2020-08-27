# c2-split-pane

## INSTALL
```
npm i c2-split-pane
```

## CODE demo.vue
```
<template>
  <c2-split-pane>
    <template v-slot:left>left</template>
    <template v-slot:right>right</template>
  </c2-split-pane>
</template>

<script>
import c2SplitPane from "c2-split-pane";

export default {
  name: "App",
  components: {
    c2SplitPane,
  },
};
</script>
```

## [DEMO](https://lancelixiang.github.io/c2-split-pane/)