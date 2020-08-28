<template>
  <div
    :class="{ 'split-pane': true, 'is-dragging': dragging }"
    @mousemove="dragMove"
    @mouseleave="dragEnd"
    @mouseup="dragEnd"
  >
    <div class="split-pane-item-left" :style="{ width: left + 'px' }">
      <slot name="left"></slot>
    </div>
    <div class="split-pane-gutter" @mousedown="dragStart"></div>
    <div class="split-pane-item-right">
      <div class="right-inner">
        <slot name="right"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "c2SplitPane",
  props: {
    type: String,
    leftWidth: { type: Number, default: 200 },
  },
  data() {
    return {
      dragging: false,
      left: 0,
    };
  },
  mounted() {
    this.left = this.leftWidth;
  },
  methods: {
    dragStart(e) {
      this.dragging = true;
      this.startX = e.pageX;
      this.startSplit = this.left || this.leftWidth;
    },
    dragMove(e) {
      if (this.dragging) {
        const dx = e.pageX - this.startX;
        this.left = this.startSplit + dx;
      }
    },
    dragEnd() {
      this.dragging = false;
    },
  },
};
</script>

<style scoped lang="less">
.split-pane {
  display: flex;
  flex-direction: row;
  &.is-dragging {
    cursor: col-resize;
  }
  &:hover {
    .split-pane-gutter:before {
      position: absolute;
      top: 38%;
      width: 17px;
      height: 20px;
      margin-left: -8.2px;
      content: "";
      background: url(./drag.svg) center center;
      background-size: 100% 100%;
    }
  }

  .split-pane-gutter {
    background: #000;
    opacity: 0.2;
    z-index: 1;
    box-sizing: border-box;
    background-clip: padding-box;
    width: 11px;
    margin: 0 5px;
    border-left: 5px solid rgba(255, 255, 255, 0);
    border-right: 5px solid rgba(255, 255, 255, 0);
    cursor: col-resize;

    &:hover,
    &:focus {
      border-left: 5px solid rgba(0, 0, 0, 0.5);
      border-right: 5px solid rgba(0, 0, 0, 0.5);
      transition: all 2s ease;
    }
  }
  .split-pane-item-right {
    flex: 1 1 auto;
    width: 0;
    .right-inner {
      width: 100%;
      overflow: auto;
    }
  }
}
</style>
