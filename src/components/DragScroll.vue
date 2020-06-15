<template>
  <div class="drag-parent" ref="parent"
       @mousedown="onDragStart"
       @mousemove="onDrag"
       @mouseup="onDragEnd"
       @mouseout="onDragEnd"
       :style="parentStyle">
    <slot />
  </div>
</template>

<script>
import throttle from 'lodash.throttle'

export default {
  data () {
    return {
      isDragging: false,
      isScrollAble: true,
      pos: {
        // scroll
        top: 0,
        left: 0,
        // mouse position
        x: 0,
        y: 0
      }
    }
  },
  computed: {
    parentStyle () {
      if (!this.isScrollAble) {
        return null
      }
      return {
        cursor: this.isDragging ? 'grabbing' : 'grab',
        userSelect: this.isDragging ? 'none' : 'text'
      }
    }
  },
  mounted () {
    this.setIsScrollAble()
    window.addEventListener('resize', this.setIsScrollAble)
  },
  destroyed () {
    window.removeEventListener('resize', this.setIsScrollAble)
  },
  methods: {
    setIsScrollAble: throttle(function () {
      const {
        clientWidth,
        clientHeight,
        scrollWidth,
        scrollHeight
      } = this.$el
      const isHorizontalScroll = scrollWidth - clientWidth > 0
      const isVerticalScroll = scrollHeight - clientHeight > 0
      this.isScrollAble = isHorizontalScroll || isVerticalScroll || false
    }, 300),
    onDragStart (e) {
      const ele = this.$el
      this.pos = {
        // 当前滚动位置
        left: ele.scrollLeft,
        top: ele.scrollTop,
        // 当前鼠标位置
        x: e.clientX,
        y: e.clientY
      }
      this.isDragging = true
    },
    onDrag: throttle(function (e) {
      if (!this.isDragging) { return }
      const ele = this.$el
      const dx = e.clientX - this.pos.x
      const dy = e.clientY - this.pos.y

      // Scroll the element
      ele.scrollTop = this.pos.top - dy
      ele.scrollLeft = this.pos.left - dx
    }, 16.666667),
    onDragEnd (e) {
      if (!this.isDragging) { return }
      this.isDragging = false
    }
  }
}
</script>

<style lang="scss" scoped>
.drag-parent {
  overflow: auto;
}
</style>
