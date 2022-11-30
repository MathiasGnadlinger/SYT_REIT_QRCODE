<template>
  <div id="app">
    <Header />
    <hr />
    <Main />
    <hr />
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';
import Main from './components/Main.vue';

export default {
  name: 'App',
  components: {
    Header,
    Footer,
    Main,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
hr {
  margin-top: 30px;
  margin-bottom: 40px;
}
body {
  /* background-color: paperwhite; */
  opacity: 0.9;
}

a {
}
</style>
