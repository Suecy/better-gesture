<template>
  <div class="press-move">
    <p>deltaX:{{deltaX}}</p>
    <p>deltaY:{{deltaY}}</p>
    <p>deltaTime:{{deltaTime}}ms</p>
    <section class="wrap">
      <div
        class="drag"
        v-gesture:pressMove="pressMove"
        :style="{transform:`translate3d(${distanceX}px,${distanceY}px,0)`}"
      ></div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'pressMove',
  data() {
    return {
      distanceX: 0,
      distanceY: 0,
      deltaX: 0,
      deltaY: 0,
      deltaTime: 0
    }
  },
  methods: {
    pressMove(evt, abc) {
      evt.preventDefault()
      this.deltaX = evt.deltaX
      this.deltaY = evt.deltaY
      this.deltaTime = evt.deltaTime
      let distanceX = this.distanceX + evt.deltaX
      let distanceY = this.distanceY + evt.deltaY
      //边界限制
      if (distanceY < -100) {
        distanceY = -100
      } else if (distanceY > 100) {
        distanceY = 100
      }
      if (distanceX < -100) {
        distanceX = -100
      } else if (distanceX > 100) {
        distanceX = 100
      }
      this.distanceX = distanceX
      this.distanceY = distanceY
    }
  }
}
</script>

<style scoped >
.press-move p {
  margin: 0;
}
.wrap {
  width: 300px;
  height: 300px;
  border: 1px solid skyblue;
  display: flex;
}
.drag {
  margin: auto;
  width: 100px;
  height: 100px;
  background: skyblue;
  cursor: pointer;
}
</style>
