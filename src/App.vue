<template>
  <div id="app">
    <Nav />
    <router-view id="app-view"/>
    <Footer class='app-footer' />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Nav from '@/components/Nav.vue' // @ is an alias to /src
import Footer from '@/components/Footer.vue'

@Component({
  components: {
    Nav,
    Footer
  }
})
export default class App extends Vue {}
</script>

<style>
@import 'components/colorVariables.css';

* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

body {
  background: var(--bg-main-dark);
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  min-height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--font-light);
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-content: center;
  align-items: center;
  min-height: 100vh;
  width: 100%;
  border: 2px solid var(--secondary-light-supertransparent);
}

#app-view {
  width: 85%;
  border: 1px solid var(--border-light-soft);
  background: var(--app-view-background);
  border-radius: 10px;
  padding: 0.5rem;
  margin: 2rem 0 5rem 0;
}

@media screen and (max-width:600px) {
  #app-view {
    width: 90%;
    margin-top: 0.5rem;
  }
}
@media screen and (max-height: 750px) {
  #app-view {
    margin-top: 1rem;
  }
}
</style>
