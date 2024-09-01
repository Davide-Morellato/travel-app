<script>
import { store } from './store.js'
import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'

export default {
  components: {
    AppHeader,
    AppFooter,
  },
  data() {
    return {
      store,
    }
  }
}

</script>

<template>

  <AppHeader></AppHeader>
  <main>
    <RouterView />
  </main>
  <AppFooter></AppFooter>

</template>

<style lang="scss">
@use './assets/style/general.scss';
@use 'bootstrap'
</style>
