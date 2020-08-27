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
