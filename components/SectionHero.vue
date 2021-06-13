<template>
  <div class="section-hero">
    <graphics-space-bg />

    <div class="tm-section-container section-container">
      <graphics-hero />

      <div class="content">
        <div class="overline tm-overline tm-medium">Welcome to Cosmos</div>
        <h1 class="title">The Internet of Blockchains</h1>
        <p class="subtitle">
          Cosmos is an ever-expanding ecosystem of interconnected apps and
          services, an Interchain built for a decentralized future.
        </p>
      </div>
    </div>
  </div>
</template>

<script></script>

<style lang="stylus" scoped>
.section-hero
  overflow hidden
  position relative
  display flex
  flex-direction column
  padding 4rem 0
  min-height 100vh
  height 100%
  background linear-gradient(191.09deg, var(--transparent) 72.09%, var(--black) 91.81%)
  text-align center
  @media $breakpoint-xsmall
    padding-top 0.75rem
  @media $breakpoint-small
    padding-bottom 0.75rem
    text-align left

.content
  position relative
  z-index 1
  @media $breakpoint-small
    display flex
    flex-direction column
    justify-content center
    height 71.875vw
    max-height 52.5rem
    padding-top 3.75rem
  @media $breakpoint-medium
    padding-top 5.125rem

.overline
  color var(--white-500)
  font-size 0.8125rem
  @media $breakpoint-medium
    font-size 1rem

.title
  max-width 24rem
  margin 1rem auto
  font-size 2.375rem
  line-height 124.7%
  letter-spacing -0.027em
  font-weight bold
  @media $breakpoint-small
    margin-left 0
    font-size 3.25rem
    font-weight 700
    letter-spacing -0.043em
  @media $breakpoint-medium
    max-width 39.375rem
    font-size 4.1875rem
    line-height 1.179
    letter-spacing -0.055em
  @media $breakpoint-large
    font-size 5.625rem
    font-weight 800
    line-height 1.12

.subtitle
  color var(--white-800)
  font-size 1rem
  line-height 1.625rem
  max-width 24rem
  margin 0 auto
  @media $breakpoint-small
    margin-left 0
  @media $breakpoint-medium
    max-width 31.5rem
    font-size 1.3125rem
    font-weight 300
    line-height 1.619
    letter-spacing -0.007em
</style>
