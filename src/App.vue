<template lang="pug">
  main
    wheel
</template>

<script>
import Wheel from './body.vue'
export default {
  name: 'app',
  components: { Wheel }
}
</script>

<style lang="sass">
*
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale

main
  text-align: center
  max-width: 1100px
  margin: 0 auto
</style>
