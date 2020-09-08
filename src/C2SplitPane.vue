<template>
  <div
    :class="{ 'split-pane': true, 'is-dragging': dragging, 'is-vertical': type==='vertical' }"
    @mousemove="dragMove"
    @mouseleave="dragEnd"
    @mouseup="dragEnd"
    ref="wrapper"
  >
    <div v-if="type==='vertical'" class="split-pane-item-up" :style="{ height: up + 'px' }">
      <div class="up-inner">
        <slot name="up"></slot>
      </div>
    </div>
    <div v-else class="split-pane-item-left" :style="{ width: left + 'px' }">
      <div class="left-inner">
        <slot name="left"></slot>
      </div>
    </div>
    <div class="split-pane-gutter" @mousedown="dragStart"></div>
    <div v-if="type==='vertical'" class="split-pane-item-down">
      <div class="down-inner">
        <slot name="down"></slot>
      </div>
    </div>
    <div v-else class="split-pane-item-right">
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
    type: { type: String, default: "horizon" }, // 分割面板类型 水平：horizon， 垂直：vertical
    leftWidth: { type: Number, default: 200 }, // 左侧面板的宽度
    upHeight: { type: Number, default: 200 }, // 上方面板的宽度
    minWidth: { type: Number, default: 50 }, // 水平面板的最小宽
    minHeight: { type: Number, default: 50 }, // 垂直面板的最小高
  },
  data() {
    return {
      dragging: false,
      left: 0,
      up: 0,
    };
  },
  created() {
    window.addEventListener("resize", this.resize, false);
  },
  mounted() {
    this.$nextTick(() => {
      this.update(this.leftWidth, this.upHeight);
    });
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.resize, false);
  },
  methods: {
    dragStart(e) {
      this.dragging = true;
      this.startX = e.pageX;
      this.startY = e.pageY;
      this.startSplitX = this.left || this.leftWidth;
      this.startSplitY = this.up || this.upHeight;
    },
    dragMove(e) {
      if (this.dragging) {
        const dx = e.pageX - this.startX;
        const dy = e.pageY - this.startY;
        const left = this.startSplitX + dx;
        const up = this.startSplitY + dy;
        this.update(left, up);
      }
    },
    dragEnd() {
      this.dragging = false;
    },
    /** 响应拖拽事件
     * @param left {number}
     * @param up   {number}
     */
    update(left, up) {
      const { offsetWidth, offsetHeight } = this.$refs.wrapper;

      if (left > this.minWidth && offsetWidth - left > this.minWidth) {
        this.left = left;
      }
      if (up > this.minHeight && offsetHeight - up > this.minHeight) {
        this.up = up;
      }
    },
    /** 响应容器resize事件 */
    resize() {
      this.$nextTick(() => {
        const { offsetWidth, offsetHeight } = this.$refs.wrapper;
        if (offsetWidth - this.left < this.minWidth) {
          this.left = offsetWidth - this.minWidth;
        }
        console.log("aaaa", offsetHeight);
        if (offsetHeight - this.up < this.minHeight) {
          this.up = offsetHeight - this.minHeight;
        }
      });
    },
  },
};
</script>

<style scoped lang="less">
.split-pane {
  position: relative;
  display: flex;
  flex-direction: row;
  &.is-vertical {
    flex-direction: column;
    &:hover > .split-pane-gutter {
      &:before {
        top: auto;
        left: 50%;
        margin-left: -10px;
        margin-top: -9px;
        transform: rotate(90deg);
      }
    }
    .split-pane-gutter {
      width: auto;
      height: 11px;
      margin: 5px 0;
      border-top: 5px solid rgba(255, 255, 255, 0);
      border-bottom: 5px solid rgba(255, 255, 255, 0);
      cursor: row-resize;
      &:hover,
      &:focus {
        border-top: 5px solid rgba(0, 0, 0, 0.5);
        border-bottom: 5px solid rgba(0, 0, 0, 0.5);
      }
    }
  }
  &.is-dragging {
    user-select: none;
    cursor: col-resize;
  }
  &:hover > .split-pane-gutter:before {
    position: absolute;
    top: 38%;
    width: 17px;
    height: 20px;
    margin-left: -8.2px;
    content: "";
    background: url(./drag.svg) center center;
    background-size: 100% 100%;
  }

  .split-pane-gutter {
    background: #ccc;
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

  .split-pane-item-left {
    .left-inner {
      width: 100%;
      height: 100%;
      overflow: auto;
    }
  }
  .split-pane-item-right {
    flex: 1 1 auto;
    width: 0;
    .right-inner {
      width: 100%;
      height: 100%;
    }
  }
  .split-pane-item-up {
    .up-inner {
      height: 100%;
      overflow: auto;
    }
  }
  .split-pane-item-down {
    flex: 1 1 auto;
    height: 0;
    .down-inner {
      height: 100%;
      overflow: auto;
    }
  }
}
</style>
