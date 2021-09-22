<template>
  <main class="main">
    <Header/>
    <Calc/>
  </main>
</template>

<script>
import Header from './Header.vue'
import Calc from './Calc.vue'

export default {
  name: 'Main',
  components: {
    Header,
    Calc
  }
}
</script>

<style scoped>
main {
width: 100%;
height: 95%;
}
</style>
