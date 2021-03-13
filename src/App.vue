<template>
  <Home />
</template>

<script>
import Home from "../src/pages/Home";
export default {
  name: "App",
  components: {
    Home,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

* h1 {
  font-size: 20px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #202124;
  color: #e5e5e5;
}
</style>
