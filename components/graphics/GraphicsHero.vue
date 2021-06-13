<template>
  <div class="graphic-hero">
    <div class="scene">
      <div class="scene-inner" :style="graphicScale">
        <graphics-planet has-green has-pulse />

        <div class="orbit">
          <div class="orbit__part"></div>
          <div class="orbit__part"></div>
          <div class="orbit__part"></div>

          <div class="line line-1"></div>
          <div class="line line-2"></div>
          <div class="line line-3"></div>

          <graphics-planet type="small" number="1" />
          <graphics-planet type="small" number="2" />
          <graphics-planet type="small" number="3" />
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="stylus" scoped>
$hexagon-size = 52px
$planet-size = $hexagon-size * 4.25
$hexagon-border-color = #0088ff
$hexagon-image-color = rgba($hexagon-border-color, 0.25)
$hexagon-green-border-color = #00ffaa
$hexagon-green-image-color = rgba($hexagon-green-border-color, 0.25)
$color-purple = #999cff

.graphic-hero
  display flex
  justify-content center
  box-sizing border-box
  margin-bottom -2rem
  margin-left -0.75rem
  margin-right -0.75rem
  font-size 0
  @media $breakpoint-xsmall
    margin-bottom -4.5625rem
  @media $breakpoint-small
    position absolute
    max-width 34.5rem
    width 100%
    top 0.75rem
    right -5.5rem
    margin 0
  @media $breakpoint-medium
    max-width none
    right auto
    left 44.7%
    width 71.875vw
    max-width 52.5rem
    transform translateX(calc((-100vw + 48rem)/7))
  @media $breakpoint-large
    left 41%
    transform none

.scene
  max-width 26rem
  width 100%
  border-radius .5rem
  @media $breakpoint-small
    max-width 34.5rem
  @media $breakpoint-medium
    max-width none
  &.debug
    border 1px dashed var(--white-500)
  &-inner
    position relative
    height 0
    padding-bottom 100%

.orbit
  position absolute
  top 0
  left 0
  width 100%
  height 100%
  animation rotateOrbit 30s linear infinite
  &__part
    position absolute
    top 50%
    left 50%
    width ($hexagon-size * 12)
    height ($hexagon-size * 12)
    margin-left ($hexagon-size * -6)
    margin-top ($hexagon-size * -6)
    border-radius 50%
    border 1px solid rgba($color-purple, 0.65)
    filter drop-shadow(0 0 4px $color-purple)
    clip-path polygon(0 0, 47.5% 0, 47.5% 47.5%, 0 47.5%)
    opacity 0
    animation initOrbitPart 1s ease-in-out 2.5s 1 normal forwards
    &:after
      content ''
      width 6px
      height 6px
      top calc(50% + 3px)
      left 0
      display block
      position absolute
      border 1px solid rgba($color-purple, 0.8)
      background-color rgba($color-purple, 1)
      border-radius 50%
      z-index 9
      animation rotateOrbitBlick 7.5s linear infinite
      transform-origin calc(100% + (52px * 6)) 0
      transform translate(-100%, 0)
    for $num in (0..2)
      &:nth-child({$num + 1})
        transform rotate(32deg + (120 * $num))
        &:after
          animation-delay 2.5s * $num
  &:before, &:after
    content ''
    position absolute
    top 50%
    left 50%
    border-radius 50%
    border 1px solid $color-purple
    filter: drop-shadow(0 0 2px white) drop-shadow(0 0 4px $color-purple)
    transform scale(0)
  &:before
    width ($hexagon-size * 16.5)
    height ($hexagon-size * 16.5)
    margin-left ($hexagon-size * -8.25)
    margin-top ($hexagon-size * -8.25)
    opacity .6
    animation initOrbit 1s ease-in-out 2s 1, pulseOrbit 4s ease-in-out 3s infinite
  &:after
    width ($hexagon-size * 17.5)
    height ($hexagon-size * 17.5)
    margin-left ($hexagon-size * -8.75)
    margin-top ($hexagon-size * -8.75)
    opacity .4
    animation initOrbit 1.2s ease-in-out 1.9s 1, pulseOrbit 4s ease-in-out 3.1s infinite

.line
  position absolute
  width $hexagon-size * 6
  height 0
  top 50%
  left 50%
  margin-left $hexagon-size * -3
  @media $breakpoint-small
    margin-left 0
    transform-origin 0
  &:before, &:after
    content ''
    position absolute
    width $hexagon-size * 1.8
    height 1px
    box-shadow:
      0 0 2px rgba(#fff, .3),
      0 0 4px rgba($hexagon-border-color, .3)
    background-position 0 0
    opacity 0
  &:before
    background rgba($hexagon-border-color, .4) linear-gradient(to left, #fff, var(--transparent) 30%)
    transform translateY(6px) translateX($hexagon-size * 2.3)
    animation:
      initLine .3s ease-in-out 1 normal forwards,
      lineBlick 1s infinite
  &:after
    background rgba($hexagon-border-color, .4) linear-gradient(to right, #fff, var(--transparent) 30%)
    transform translateY(-6px) translateX($hexagon-size * 2.3)
    animation:
      initLine .3s ease-in-out 1 normal forwards,
      lineBlick 1s infinite reverse
  for $num in (0..2)
    &-{$num + 1}
      transform rotate(77deg + (120 * $num))
      &:before
        animation-delay 1.1s + (0.2 * $num)
      &:after
        animation-delay 1.3s + (0.2 * $num)

@keyframes initOrbit
  from
    transform scale(.1)
  to
    transform scale(1)

@keyframes initOrbitPart
  from
    opacity 0
  to
    opacity 1

@keyframes rotateOrbit
  from
    transform rotate(0deg)
  to
    transform rotate(360deg)

@keyframes rotateOrbitBlick
  0%
    transform translate(-100%, 0) rotate(0deg)
  100%
    transform translate(-100%, 0) rotate(360deg)

@keyframes pulseOrbit
  0%, 100%
    transform scale(1)
  50%
    transform scale(0.98)

@keyframes pulseMainOrbit
  0%
    filter drop-shadow(0 0 0 rgba(#fff, 0)) drop-shadow(0 0 0 rgba($color-purple, 0))
  70%
    filter drop-shadow(0 0 .5rem rgba(#fff, 0.4)) drop-shadow(0 0 1rem rgba($color-purple, 0.8))
  100%
    filter drop-shadow(0 0 0 rgba(#fff, 0)) drop-shadow(0 0 0 rgba($color-purple, 0))

@keyframes initLine
  100%
    opacity 1

@keyframes lineBlick
  100%
    background-position ($hexagon-size * 1.8) 0
</style>

<script>
export default {
  data: () => ({
    loading: true,
    containerInfo: {
      width: 0,
      scene: '',
    },
    animationInfo: {
      width: 900,
    },
  }),
  computed: {
    graphicScale() {
      const scale = this.containerInfo.width / this.animationInfo.width;
      return {
        transform: `scale(${scale})`,
      };
    },
  },
  mounted() {
    this.containerInfo.scene = this.$el.children[0];
    window.addEventListener('resize', () => this.resizeHandler());
    this.resizeHandler();
  },
  methods: {
    resizeHandler() {
      this.containerInfo.width = this.containerInfo.scene.clientWidth;
    },
  },
};
</script>
