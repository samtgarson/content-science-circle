<template lang="pug">
.wrapper(:class="[side, { downwards }]")
  transition(name="slide")
    box(v-if="active", v-bind="active", @reset="active = null", :style="style")
  svg(viewBox="0 0 826 826", :class="{ active: !!active }")
    defs
      linearGradient#linearGradient-1(x1="0%", y1="50.0067595%", x2="100.004308%", y2="50.0067595%")
        stop(stop-color="#73FFBD", offset="0%")
        stop(stop-color="#FFFFFF", offset="100%")
      linearGradient#linearGradient-2(x1="0%", y1="50%", x2="100%", y2="50%")
        stop(stop-color="#5EEFAA", offset="0%")
        stop(stop-color="#FFFFFF", offset="100%")
      linearGradient#linearGradient-3(x1="-0.0127773656%", y1="50.0051493%", x2="99.9871453%", y2="50.0051493%")
        stop(stop-color="#41D890", offset="0%")
        stop(stop-color="#FFFFFF", offset="100%")
      linearGradient#linearGradient-4(x1="-0.00424114361%", y1="50.0016897%", x2="99.9897963%", y2="50.0016897%")
        stop(stop-color="#2DC97E", offset="0%")
        stop(stop-color="#FFFFFF", offset="100%")
      linearGradient#linearGradient-5(x1="0%", y1="50.0098438%", x2="99.997006%", y2="50.0098438%")
        stop(stop-color="#1ABA6D", offset="0%")
        stop(stop-color="#FFFFFF", offset="100%")
      linearGradient#linearGradient-6(x1="7.73651674e-05%", y1="50%", x2="100.012779%", y2="50%")
        stop(stop-color="#07AA5C", offset="0%")
        stop(stop-color="#FFFFFF", offset="100%")
    circle(fill="#FFFFFF" cx="413" cy="413" r="413")
    div(
      v-for="segment in segments",
      :is="segment.name",
      ref="segments",
      @mousedown.native="activate(segment, $event)",
      :active="segment.active")
    text
      tspan(x="143.88", y="626.22") CONTENT
      tspan(x="143.88", y="650.22") DISTRIBUTION
    text
      tspan.numbers(x="143.45", y="600.71") 05.
    text
      tspan(x="446.88", y="721.22") CONTENT
      tspan(x="446.88", y="745.22") INTEGRATION
    text
      tspan.numbers(x="446.45", y="695.71") 04.
    text
      tspan(x="664.88", y="519.22") CONTENT
      tspan(x="664.88", y="543.22") CREATION
    text
      tspan.numbers(x="664.45", y="493.71") 03.
    text
      tspan(x="61.88", y="338.22") MEASURING
      tspan(x="61.88", y="362.22") IMPACT
    text
      tspan(x="575.88", y="223.22") COLLECTING
      tspan(x="575.88", y="247.22") DATA
    text
      tspan.numbers(x="575.45", y="197.71") 02.
    text
      tspan.numbers(x="61.45", y="312.71") 06.
    text
      tspan(x="300.88", y="123.22") SETTING
      tspan(x="300.88", y="147.22") THE GOAL
    text
      tspan.numbers(x="300.45", y="97.71") 01.
    g.title(transform="translate(227.000000, 394.000000)")
      text(font-size="31.2119988")
        tspan(x="1.18646397", y="30") Content Science Circle
      text(font-size="16.6463994")
        tspan(x="360.203113", y="17.0404") ®
</template>

<script>
import One from './segments/one.vue'
import Two from './segments/two.vue'
import Three from './segments/three.vue'
import Four from './segments/four.vue'
import Five from './segments/five.vue'
import Six from './segments/six.vue'
import segments from "./text"
import Box from "./box.vue"

export default {
  components: { One, Two, Three, Four, Five, Six, Box },
  name: 'body',
  data: () => ({ active: false, side: '', style: {}, downwards: false }),
  mounted () {
    setTimeout(() => {
      this.activate(this.segments[0], {
        target: this.$refs.segments[0].$el
      })
    }, 1000)
  },
  watch: {
    active (n) {
      if (!n) return this.side = ''
    }
  },
  methods: {
    activate (segment, { target }) {
      this.active = segment
      this.side = segment.index > 0 && segment.index < 4 ? 'left' : 'right'
      this.downwards = [3, 4].includes(segment.index)

      const { top, height } = target.getBoundingClientRect()
      if (this.downwards) {
        this.style = { bottom: `-${top + height}px` }
      } else {
        this.style = { top: `${top}px` }
      }
    }
  },
  computed: {
    segments () {
      return segments.map((segment, index) => ({
        ...segment,
        index,
        active: this.active && this.active.name === segment.name
      }))
    }
  }
}
</script>

<style lang="sass" scoped>
$bg: (a: #6cffb9, b: #5eefaa, c: #41d890, d: #2dc97e, e: #1aba6d, f: #07aa5c)

@each $class, $colour in $bg
  .#{$class}
    fill: #{$colour}

.wrapper
  font-family: Montserrat-Bold, Montserrat
  font-weight: 700
  display: flex
  justify-content: space-around

.segment
  cursor: pointer

text
  fill: white
  pointer-events: none

.title text
  fill: black

.numbers
  font-size: 40px

svg
  transition: filter .5s ease
  width: 100%
  max-width: 500px
  position: relative
  min-height: 650px
  margin: 0 auto
  z-index: 1

  @media (min-width: 1000px)
    position: absolute
    transition: transform .2s ease
    left: 50%
    transform: translateX(-50%)

    .left &
      transform: translateX(calc(-50% - 250px))

    .right &
      transform: translateX(calc(-50% + 250px))

  &.active
    @media (max-width: 1000px)
      filter: blur(7px)

.box
  position: absolute
  background-color: rgba(white, .9)
  padding: 50px
  margin: 0 -20px
  z-index: 2

  @media (max-width: 1000px)
    top: 0 !important
    bottom: 0 !important
    left: 0
    right: 0
    display: flex
    flex-flow: column
    align-items: left
    justify-content: center

  @media (min-width: 1000px)
    z-index: 0
    margin: 0
    left: 50%
    transform: translateX(-50%)
    width: 350px
    background: transparent
    transition: transform .2s ease, top .2s ease, opacity .1s ease-out
    padding-top: 32px

    .left &
      transform: translateX(calc(-50% + 250px))

    .right &
      transform: translateX(calc(-50% - 250px))


</style>
