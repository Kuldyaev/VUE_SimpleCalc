<template>
  <footer class="footer">
    <h3>Created by <span><a href="http://www.kuldyaev.ru">Viacheslav Kuldyaev</a></span></h3>
  </footer>
</template>

<script>
export default {
  name: 'Footer'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
footer{
  width: 100%;
  height: 50px;
  background-color: #42b983;
  color: white;
  display: flex;
  justify-content: end;
  align-items: center;
}
a{
  color: white;
}
h3{
  margin-right: 15px;
}
@media screen and (max-width: 408px)  {
  h3{font-size: 12px;}
}
</style>
