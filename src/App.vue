<template>
  <div id="app">
    <Game/>
  </div>
</template>

<script>
import Game from "./components/Game";
export default {
  name: 'App',
  components: {Game}
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #6c98c7;
  background: #333333;
  min-height: 100vh;
}
</style>
