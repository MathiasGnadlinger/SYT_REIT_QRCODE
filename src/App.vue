<template>
  <div id="app">
    <img alt="Vue logo" src="https://vuejs.org/images/logo.png" />

    <Suspense>
      <template #default>
        <UserSelectList />
      </template>
      <template #fallback>
        <span>Loading...</span>
      </template>
    </Suspense>

    <UserList />
  </div>
</template>

<script>
import Footer from './components/Footer.vue';
import Main from './components/Main.vue';
import Header from './components/Header.vue';

export default {
  name: 'App',
  components: {
    Footer,
    Header,
    Main,
  },
};
</script>

<style>
img {
  width: 5em;
  display: block;
  margin-left: auto;
  margin-right: auto;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  //text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
