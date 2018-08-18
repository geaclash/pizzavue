
<template>
  <v-app>
    <component v-bind:is="layout"></component>
  </v-app>
</template>

<script>
import AppLayout from './layouts/AppLayout'
import BlankLayout from './layouts/BlankLayout'
import FrontendLayout from './layouts/FrontendLayout'
export default {
  computed: {
    layout () {
      return this.$store.getters.layout
    }
  },
  components: {
    'app-layout': AppLayout,
    'frontend-layout': FrontendLayout,
    'blank-layout': FrontendLayout

    // define as many layouts you want for the application
  }
}
</script>