<template>
  <v-app dark>
    <h1 class="centered" v-if="this.error.statusCode == 404">
      Oops. That page doesn't exist.
    </h1>
  </v-app>
</template>

<script>
export default {
  layout: 'empty',
  props: {
    error: {
      type: Object,
      default: null
    }
  },
}
</script>

<style scoped>
h1 {
  font-size: 20px;
}

.centered {
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  position: fixed;
}
</style>
