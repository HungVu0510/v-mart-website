<template>
  <v-app dark :style="{ backgroundColor: $vuetify.theme.dark ? '#0a0514' : 'white' }">
    <v-main>
      <Nav />
      <Nuxt />
      <Footer class="fixed bottom-0"></Footer>
      <ScrollTop />
    </v-main>
  </v-app>
</template>

<script>
export default {

}
</script>

<style>

</style>