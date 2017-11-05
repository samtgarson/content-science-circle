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

html,
body
  margin: 0
  padding: 0

main
  position: relative
  text-align: center
  max-width: 1000px
  margin: 0 auto

.fade-enter-active, .fade-leave-active
  transition: opacity .2s

.fade-enter, .fade-leave-active
  opacity: 0

.slide-enter-active, .slide-leave-active
  transition: opacity .2s, transform .3s ease-out

.slide-enter, .slide-leave-active
  opacity: 0
  transform: translateY(8px)
</style>
