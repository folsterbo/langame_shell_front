<template>
  <v-app>
    <v-navigation-drawer app>
      <the-menu></the-menu>
    </v-navigation-drawer>
    <v-main>
      <v-container class="pa-8">
        <router-view></router-view>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>

import TheMenu from './components/layout/TheMenu.vue'

export default {
  name: 'App',
  components: { TheMenu },
  data: function () {
    return {
    }
  },
  computed: {
  },
  methods: {
  }
};
</script>

<style lang='scss'>
@import 'App.scss';
</style>
