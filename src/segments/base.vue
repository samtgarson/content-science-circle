<template lang="pug">
  g.base-segment(:class="{ active }")
    slot
    transition(name="fade")
      template(v-if="active")
        slot(name="stroke")
</template>

<script>
export default {
  name: 'base',
  props: {
    active: Boolean
  }
}
</script>

<style lang="sass" scoped>

.base-segment
  overflow: hidden

  & >>> .gradient
    opacity: 0.3

  & >>> .hover
    transition: opacity .2s ease
    opacity: 0
    pointer-events: none
    // fill: #6AD9B1

  & >>> .stroke
    transition: fill .3s ease

  &:active >>> .stroke
    fill: rgba(black, 0.1)


  &:not(.active) >>> .shape
    &:hover + .hover
      opacity: 1
</style>
