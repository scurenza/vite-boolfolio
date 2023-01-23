<script>
import AppHeader from './components/AppHeader.vue';
// import AppMain from './components/AppMain.vue';

export default {
  name: 'App',
  components: {
    // AppMain,
    AppHeader
  }
}

</script>

<template>
  <AppHeader />
  <!-- <main>
    <AppMain />
  </main> -->
  <router-view></router-view>
</template>

<style lang="scss">
@use "./styles/general.scss" as *;
</style>