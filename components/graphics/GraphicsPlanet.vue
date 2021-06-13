<template>
  <div
    :class="[
      'planet-container',
      `planet-container--${type}`,
      !!number && `planet-container--small-${number}`,
    ]"
  >
    <div
      :class="[
        'planet',
        `planet--${type}`,
        !!number && `planet--small-${number}`,
      ]"
    >
      <div class="planet__inner"></div>
    </div>

    <div
      :class="[
        'hexagon-container',
        `hexagon-container--${type}`,
        !!number && `hexagon-container--small-${number}`,
      ]"
    >
      <div class="hexagon">
        <div :class="['hexagon__inner', !!hasGreen && 'hexagon__inner--green']">
          <logo-tendermint v-if="hasGreen" class="logo logo-tendermint" />
        </div>
      </div>

      <div :class="['hexagon', !!hasPulse && 'hexagon-pulse']">
        <div class="hexagon__inner"></div>
      </div>
      <div :class="['hexagon', !!hasPulse && 'hexagon-pulse']">
        <div class="hexagon__inner"></div>
      </div>
      <div :class="['hexagon', !!hasPulse && 'hexagon-pulse']">
        <div class="hexagon__inner"></div>
      </div>
      <div :class="['hexagon', !!hasPulse && 'hexagon-pulse']">
        <div class="hexagon__inner"></div>
      </div>
      <div :class="['hexagon', !!hasPulse && 'hexagon-pulse']">
        <div class="hexagon__inner"></div>
      </div>
      <div :class="['hexagon', !!hasPulse && 'hexagon-pulse']">
        <div class="hexagon__inner"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    type: {
      /**
       * `main` | `small`
       */
      type: String,
      default: 'main',
    },
    /**
     * number: `1` | `2` | `3`
     */
    number: {
      type: String,
      default: '',
    },
    /**
     * hasPulse
     */
    hasPulse: {
      type: Boolean,
      default: false,
    },
    /**
     * hasGreen
     */
    hasGreen: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style lang="stylus" scoped>
$hexagon-size = 52px
$planet-size = $hexagon-size * 4.25
$hexagon-border-color = #0088ff
$hexagon-image-color = rgba($hexagon-border-color, 0.25)
$hexagon-green-border-color = #00ffaa
$hexagon-green-image-color = rgba($hexagon-green-border-color, 0.25)
$color-purple = #999cff
$color-tendermint = #54b735

.logo-tendermint
  position absolute
  top 50%
  left 50%
  width 36px
  height 36px
  color: $color-tendermint
  transform translate(-50%, -50%) scale(0)
  animation: initLogo 1s cubic-bezier(0.32, 0, 0.67, 0) 1.5s 1 normal forwards

.planet-container
  position: absolute
  top: 50%
  left: 50%
  width: $planet-size
  height: $planet-size
  margin-left: ($planet-size / 2 * -1)
  margin-top: ($planet-size / 2 * -1)
  &--small
    transform scale(.75)
    animation: rotatePlanet 30s linear infinite
    &-1
      margin-left: ($planet-size * -1.85)
      margin-top: ($planet-size * -0.925)
      .planet,
      .hexagon-container
        animation-delay: 1.2s
        &__inner
          animation-delay: 1.2s
    &-2
      margin-left: ($planet-size * 0.5)
      margin-top: ($planet-size * -1.45)
      .planet,
      .hexagon-container
        animation-delay: 1.5s
        &__inner
          animation-delay: 1.5s
    &-3
      margin-left: ($planet-size * -0.2)
      margin-top: ($planet-size * 0.85)
      .planet,
      .hexagon-container
        animation-delay: 1.8s
        &__inner
          animation-delay: 1.8s

.planet
  position: relative
  width: $planet-size
  height: $planet-size
  background-color: transparent
  border-radius: 50%
  border: 2px solid rgba($hexagon-border-color, 0.5)
  box-shadow: 0 0 .25rem rgba(white, 0.2), 0 0 .75rem rgba($hexagon-border-color, 0.2)
  opacity: 0
  animation: planetInit 2s ease-in-out 1s 1 normal forwards, scaleInit 2s ease-in-out 1s 1 normal forwards
  &--main
    box-shadow: 0 0 0 rgba(204, 169, 44, 0.4)
    animation: planetInit 2s ease-in-out 1s 1 normal forwards, scaleInit 2s ease-in-out 1s 1 normal forwards, pulse 2s infinite
    &:before
      content: ''
      width: $planet-size
      height: $planet-size
      display: block
      position: absolute
      border: 2px solid rgba($hexagon-border-color, 0.6)
      border-radius: 50%
      top: -2px
      left: -2px
      box-sizing: border-box
      clip-path: polygon(0 0, 0 35px, 35px 35px, 35px 0)
      z-index: 10
      animation: rotate 3s linear infinite
    &:after
      content: '';
      width: $planet-size
      height: $planet-size
      display: block;
      position: absolute;
      border: 2px solid rgba($hexagon-border-color, .8);
      border-radius: 50%;
      top: -2px;
      left: -2px;
      box-sizing: border-box
      clip-path: polygon(0 0, 234px 0, 234px 175px, 0 175px)
      z-index: 9
      animation: rotate2 3s linear infinite
  &__inner
    position: absolute
    top: 0
    left: 0
    width: 100%
    height: 100%
    border-radius: 50%
    animation: planetInnerInit 2s ease-in-out 1s 1 normal forwards
    box-shadow: inset 0 0 ($hexagon-size / 3) rgba($hexagon-border-color, 0.4), inset ($hexagon-size / 4) ($hexagon-size / 4) ($hexagon-size / 2) rgba($hexagon-border-color, 0.2)

.hexagon-container
  position: absolute
  top: 0
  left: 0
  padding: 0
  margin: 0
  width: $planet-size
  height: $planet-size
  border-radius: 50%
  animation: scaleInit 2s ease-in-out 1s 1 normal forwards

.hexagon
  position: absolute
  top: 50%
  left: 50%
  margin-top: ($hexagon-size / -2)
  margin-left: ($hexagon-size / -2)
  list-style: none
  font-size: 0
  &__inner
    width: ($hexagon-size + 2)
    height: ($hexagon-size - 2)
    position: relative
    text-align: center
    z-index: 1
    clip-path: polygon(25% 0%, 75% 0%, 100% 50%, 75% 100%, 25% 100%, 0% 50%)
    background-image: linear-gradient(61.5deg, $hexagon-border-color 20%, transparent 20%, transparent 83.5%, $hexagon-border-color 83.5%), linear-gradient(-61.5deg, $hexagon-border-color 18%, transparent 18%, transparent 81%, $hexagon-border-color 81%), linear-gradient(0, $hexagon-border-color 5.5%, transparent 5.5%, transparent 98.5%, $hexagon-border-color 98.5%)
    background-size: $hexagon-size $hexagon-size
    opacity: 0
    &--green
      background-image: linear-gradient(61.5deg, $hexagon-green-border-color 20%, transparent 20%, transparent 83.5%, $hexagon-green-border-color 83.5%), linear-gradient(-61.5deg, $hexagon-green-border-color 18%, transparent 18%, transparent 81%, $hexagon-green-border-color 81%), linear-gradient(0, $hexagon-green-border-color 5.5%, transparent 5.5%, transparent 98.5%, $hexagon-green-border-color 98.5%)

$hexagones = ( ( 1 0 0 ) ( 2 (($hexagon-size - 2) * -0.55) (($hexagon-size + 2) * -0.85) ) ( 3 (($hexagon-size - 2) * -1.1) 0 ) ( 4 (($hexagon-size - 2) * -0.55) (($hexagon-size + 2) * 0.85) ) ( 5 (($hexagon-size - 2) * 0.55) (($hexagon-size + 2) * 0.85) ) ( 6 (($hexagon-size - 2) * 1.1) 0 ) ( 7 (($hexagon-size - 2) * 0.55) (($hexagon-size + 2) * -0.85) ) )

$time = 3s
$delay = ($time / 14)
for $num in (0..6)
  .planet-container--main
    .hexagon
      &-pulse
        &:nth-child({$num + 1})
          animation: shadow 0.75s ease-in-out 0.5s 1 normal, pulseHexagon $time ease-in-out $delay * $num infinite
      &:nth-child({$num + 1})
        transform: translate($hexagones[$num][2], $hexagones[$num][1])
        animation-delay: $delay * $num
        .hexagon__inner
          animation: init ($time / 3) ease-in-out 1 normal forwards
          animation-delay: (($delay * $num) / 6)
          &--green
            animation-name: init-green

for $index in (0..6)
  for $i in (1..3)
    .planet-container--small-{$i}
      .hexagon
        &:nth-child({$index + 1})
          transform: translate($hexagones[$index][2], $hexagones[$index][1])
          animation-delay: $delay * $index + 0.3s * $i
          .hexagon__inner
            animation: init ($time / 3) ease-in-out 1 normal forwards
            animation-delay: (($delay * $index) / 6) + 0.3 * $i

@keyframes initLogo
  100%
    transform: translate(-50%, -50%) scale(1)

@keyframes rotatePlanet
  from
    transform: rotate(360deg) scale(.7)
  to
    transform: rotate(0) scale(.7)

@keyframes planetInit
  0%
    opacity: 0;
  75%, 100%
    opacity: 1;

@keyframes scaleInit
  0%, 100%
    transform: scale(1);
  75%
    transform: scale(0.75);

@keyframes pulse
  0%
    box-shadow: 0 0 0 0 rgba($hexagon-border-color, 0.4), 0 0 0 0 rgba($hexagon-border-color, 0.4);
  70%
    box-shadow: 0 0 0 .3rem rgba($hexagon-border-color, 0), 0 0 0 1rem rgba($hexagon-border-color, 0);
  100%
    box-shadow: 0 0 0 0 rgba($hexagon-border-color, 0), 0 0 0 0 rgba($hexagon-border-color, 0);

@keyframes rotate
  0%
    transform: rotate(0);
    clip-path: polygon(0 0, 0 35px, 35px 35px, 35px 0)
  50%
    clip-path: polygon(0 0, 0 40px, 40px 40px, 40px 0)
  100%
    transform: rotate(360deg);
    clip-path: polygon(0 0, 0 35px, 35px 35px, 35px 0)

@keyframes rotate2
  0%
    transform: rotate(0);
    clip-path: polygon(0 0, 164px 0, 164px 150px, 0 150px)
  50%
    transform: rotate(360deg);
    clip-path: polygon(0 0, 164px 0, 164px 0, 0 0)
  100%
    transform: rotate(720deg);
    clip-path: polygon(0 0, 164px 0, 164px 150px, 0 150px)

@keyframes planetInnerInit
  0%, 100%
    background-color: rgba($hexagon-border-color, 0);
  75%
    background-color: rgba($hexagon-border-color, .4);

@keyframes shadow
  0%, 100%
    filter: drop-shadow(0 0 .5rem rgba(#fff, 0));
  50%
    filter: drop-shadow(0 0 .5rem #fff);

@keyframes init
  0%
    transform: scale(0.5) rotate(-180deg);
    opacity: 0;
    background-color: rgba($hexagon-image-color, 0);
  50%
    transform: scale(1) rotate(0);
    opacity: 1;
    background-color: rgba($hexagon-image-color, 0);
  100%
    opacity: 1;
    transform: rotateY(2.5turn);
    background-color: $hexagon-image-color;

@keyframes init-green
  0%
    transform: scale(0.5) rotate(-90deg);
    opacity: 0;
    background-color: rgba($hexagon-green-image-color, 0);
  50%
    transform: scale(1) rotate(0);
    opacity: 1;
    background-color: rgba($hexagon-green-image-color, 0);
  100%
    opacity: 1;
    transform: rotateY(2.5turn);
    background-color: $hexagon-green-image-color;

@keyframes pulseHexagon
  0%
    filter: drop-shadow(0 0 .5rem rgba(#fff, .5));
  15%,
  50%
    filter: drop-shadow(0 0 .5rem rgba(#fff, 0));
  65%
    filter: drop-shadow(0 0 .5rem rgba(#fff, .5));
</style>
