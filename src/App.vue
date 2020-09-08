<template>
  <c2-split-pane>
    <template v-slot:left>
      <div class="left">left left left left</div>
    </template>
    <template v-slot:right>
      <c2-split-pane type="vertical">
        <template v-slot:up>
          <div class="up">up</div>
        </template>
        <template v-slot:down>
          <div class="down">down</div>
        </template>
      </c2-split-pane>
    </template>
  </c2-split-pane>
</template>

<script>
import c2SplitPane from "./C2SplitPane";

export default {
  name: "App",
  components: {
    c2SplitPane,
  },
};
</script>
<style lang="less" scoped>
.left {
  height: calc(100vh - 300px);
  background-color: aquamarine;
}

.split-pane .split-pane {
  height: 100%;
}
.up {
  height: 100%;
  min-height: 100px;
  background-color: blueviolet;
}
.down {
  height: 100%;
  min-height: 250px;
  min-width: 750px;
  background-color: cornflowerblue;
}
</style>>
