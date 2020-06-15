<template>
  <div class="container">
    <DragScroll
      class="dragscroll"
    >
      <div class="dragscroll-inner">Vue DragScroll!</div>
    </DragScroll>
    <p class="description">Drag to Scroll!</p>
    <div class="buttons">
      <a href="https://github.com/koucxz/vue-dragscroll-lite" target="_blank">Download</a>
    </div>
  </div>
</template>

<script>
/* eslint-disable no-param-reassign,no-unused-expressions,no-console */
import DragScroll from '@/components/DragScroll.vue'

export default {
  name: 'app',
  components: {
    DragScroll
  },
  data: () => ({
    states: {
      scalable: 'Scalable',
      resizable: 'Resizable',
      warpable: 'Warpable'
    },
    currentState: 'scalable'
  }),
  methods: {
    clearAllStates () {
      Object.keys(this.states).forEach((key) => {
        this.dragscroll[key] = false
      })
    }
  },
  watch: {
    currentState (newState) {
      this.clearAllStates()
      this.dragscroll[newState] = true
    }
  }
}
</script>

<style lang="scss">
  @import url("https://fonts.googleapis.com/css?family=Open+Sans:300,400,600&display=swap");
  @import url("https://fonts.googleapis.com/css?family=Roboto:100&display=swap");
  html, body {
    font-family: "Open Sans", sans-serif;
    position: relative;
    margin: 0;
    padding: 0;
    height: 100%;
    color: #333;
    letter-spacing: 1px;
    background: #f5f5f5;
    font-weight: 300;
  }

  a {
    text-decoration: none;
    color: #333;
  }

  .container {
    position: relative;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }

  .dragscroll {
    font-family: "Roboto", sans-serif;
    position: relative;
    width: 300px;
    height: 200px;
    font-size: 40px;
    margin: 0 auto;
    font-weight: 100;
    letter-spacing: 1px;
  }

  .dragscroll-inner {
    margin-top: 60px;
    width: 200%;
    height: 200%;
  }

  .description {
    text-align: center;
  }

  .buttons {
    margin: 0;
    padding: 10px;
    text-align: center;
  }

  .buttons a {
    display: inline-block;
    position: relative;
    margin: 5px;
    padding: 12px 30px;
    border: 1px solid #4a4a4a;
    box-sizing: border-box;
    min-width: 140px;
    color: #4a4a4a;
    text-align: center;
    transition: all ease 0.5s;
    text-decoration: none;
  }

  .buttons a:hover, .buttons a.selected {
    color: #fff;
    background: #4a4a4a;
  }
</style>
