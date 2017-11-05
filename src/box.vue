<template lang="pug">
  .box
    img(src="./assets/text-box.svg")
    h2
      span {{ number }}.
      | {{ title }}
    p(v-html="text")
    button(@click="$emit('reset')") Back
</template>

<script>
export default {
  name: 'box',
  props: {
    text: String,
    title: String,
    number: String
  },
}
</script>

<style lang="sass" scoped>
.box
  text-align: left

h2
  text-transform: uppercase

  span
    color: #59FDB1
    &::after
      content: '\00a0'

p
  font-family: 'Playfair Display', serif
  font-weight: normal
  line-height: 150%

button
  font-family: Montserrat-Bold, Montserrat
  font-weight: 700
  text-transform: uppercase
  border: 0
  padding: 0
  font-size: 1em
  background: transparent

img
  @media (max-width: 1000px)
    display: none

  position: absolute
  z-index: -1
  left: 0px
  top: 8px
  width: 700px

  .left &
    left: auto
    right: 25px
    transform: scaleX(-1)

  .downwards &
    bottom: 8px
    top: auto
    transform: scaleY(-1)

  .downwards.left &
    transform: scale(-1)
</style>
