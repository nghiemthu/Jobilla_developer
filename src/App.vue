<template>
  <div id="app">
    <app-nav></app-nav>
    <router-view/>
  </div>
</template>

<script>
import AppNav from './components/AppNav';

export default {
  name: 'app',
  components: { AppNav },
};
</script>

<style lang="scss" scoped>
  @import './assets/style/app.scss'
</style>
