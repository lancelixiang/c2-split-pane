<template>
  <c2-split-pane>
    <template #left="left">
      <div class="left">left {{left.width}}</div>
    </template>
    <template #right="right">
      <c2-split-pane type="vertical">
        <template #up="up">
          <div class="up">right up {{right.width}}*{{up.height}}</div>
        </template>
        <template #down="down">
          <div class="down">
            <c2-split-pane>
              <template #left="downLeft">
                <div class="down-left">down-left {{downLeft.width}}*{{down.height}}</div>
              </template>
              <template #right="downRight">
                <div class="down-right">
                  down-right {{downRight.width}}*{{down.height}}
                </div>
              </template>
            </c2-split-pane>
          </div>
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
  height: 100%;
  background-color: aquamarine;
}

.right-inner > .split-pane {
  /** 二级分割面板容器要设置高度 */
  height: calc(100vh - 100px);
}
.down > .split-pane {
  /** 三级分割面板容器要设置高度 */
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
  min-width: 450px;
}
.down-left {
  height: 100%;
  background-color: cornflowerblue;
}
.down-right {
  height: 100%;
  background-color: wheat;
}
</style>>
