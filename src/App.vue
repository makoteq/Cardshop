<template>
  <div id="app">
    <navbar />
    <router-view />
    <footerbar />
  </div>
</template>
<script>
// @ is an alias to /src
import navbar from "@/components/navbar.vue";

import footerbar from "@/components/footerbar.vue";

export default {
  name: "App",
  components: {
    navbar,
    footerbar
  }
};
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
