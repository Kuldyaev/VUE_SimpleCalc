<template>
  <section class="main-window">
    <CalcWindow/>
  </section>
</template>

<script>
import CalcWindow from './CalcWindow.vue'

export default {
  name: 'Calc',
  components: {
    CalcWindow
  }
}
</script>

<style scoped>
section {
  width: 100%;
  height: 95%;
  background-color:  #F9F9F9;
}
</style>
