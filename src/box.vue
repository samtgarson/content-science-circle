<template lang="pug">
  .box
    h2 {{ title }}
    p(v-html="text")
</template>

<script>
export default {
  name: 'box',
  props: {
    text: {
      type: String,
      required: true
    },
    title: {
      type: String,
      required: true
    }
  },
}
</script>

<style lang="sass" scoped>
.box
  text-align: left
  width: 350px

h2
  text-transform: uppercase

p
  font-family: 'Playfair Display', serif
  font-weight: normal
  line-height: 150%
</style>
