<template>
  <div id="app" class="container">
    <router-view />
  </div>
</template>

<script>
export default {
  mounted() {
      let da = document.getElementsByTagName('span');
      console.log(da.item())
      for(let el of da){
        console.log(el)
      }
  }      
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
