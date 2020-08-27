# c2-split-pane

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

# INSTALL
```
npm i c2-split-pane
```

# CODE demo.vue
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

# DEMO []