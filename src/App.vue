<template>
  <div id="app">
    <Header />
    <router-view />
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    Header,
    Footer,
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto+Condensed&display=swap');
* {
  font-family: 'Roboto Condensed', sans-serif;
  // margin: 0;
  // padding: 0;
}
  html,body {
    margin: 0;
    padding: 0;
    height: 100%;
  }
  #app {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    min-width: 720px;
    min-height: 100%;
  }
</style>
