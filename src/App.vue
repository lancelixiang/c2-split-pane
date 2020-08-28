<template>
  <c2-split-pane>
    <template v-slot:left>
      <div class="left">left</div>
    </template>
    <template v-slot:right>
      <div class="right">right</div>
    </template>
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
<style scoped>
.left {
  height: 600px;
  margin-right: 10px;
  background-color: aquamarine;
}
.right {
  width: 750px;
  margin-left: 10px;
  background-color: darkcyan;
}
</style>>
