<template>
  <div class="nav-container" :class="{ 'nav-opened': isOpenMenu }">
    <div class="tm-section-container">
      <nav class="nav" role="navigation">
        <div class="nav-main">
          <NuxtLink to="/" class="nav-link-logo">
            <logo-cosmos-wordmark class="logo logo-cosmos" />
            <span class="sr-only">Cosmos</span>
          </NuxtLink>

          <div class="nav-slider">
            <ul class="nav-list">
              <li class="nav-list__item">
                <NuxtLink to="/learn" class="nav-link text tm-rf-1 tm-medium">
                  Learn</NuxtLink
                >
              </li>
              <li class="nav-list__item">
                <NuxtLink to="/build" class="nav-link text tm-rf-1 tm-medium">
                  Build</NuxtLink
                >
              </li>
              <li class="nav-list__item">
                <NuxtLink to="/explore" class="nav-link text tm-rf-1 tm-medium">
                  Explore</NuxtLink
                >
              </li>
            </ul>
          </div>

          <div class="nav-slider">
            <tm-button
              to-link="internal"
              to="/start"
              size="xs"
              color="var(--black)"
              background-color="var(--white-800)"
            >
              Start now
            </tm-button>
          </div>
        </div>

        <tm-burger
          class="nav-burger"
          :class="{ 'nav-opened': isOpenMenu }"
          @click.native.prevent="toggleMenu"
        />
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    isOpenMenu: false,
  }),
  methods: {
    toggleMenu() {
      this.isOpenMenu = !this.isOpenMenu;
    },
  },
};
</script>

<style lang="stylus" scoped>
.nav-container
  position absolute
  z-index 99
  top 0
  left 0
  right 0

.nav
  display flex
  justify-content space-between
  width 100%
  padding-top 1.4375rem
  @media $breakpoint-xsmall
    padding 1.3125rem 0

  &-main
    padding-bottom var(--spacing-7)
    @media $breakpoint-xsmall
      display flex
      align-items center
      justify-content space-between
      width 100%
      padding-bottom 0
    &:before
      content ''
      position absolute
      z-index -1
      top 0
      left 0
      right 0
      height 100%
      width 100%
      opacity 0
      background-color var(--primary-100)
      transform scale(0.75) translate3d(0,0,0)
      transform-origin top left
      transition transform var(--default-transition-duration) var(--bezier-transition-function),
        opacity var(--default-transition-duration) var(--bezier-transition-function);
      @media $breakpoint-xsmall
        display none
      .nav-opened &
        opacity 1
        transform scale(1)

  &-slider
    display none
    padding var(--spacing-4) 0
    @media $breakpoint-xsmall
      display block
      padding 0
    .nav-opened &
      animation appear var(--default-transition-duration--2) var(--bezier-transition-function)
      display: block

@keyframes appear
  0%, 35%
    opacity 0

.logo-cosmos
  width auto
  height 1.1rem
  color: var(--white)

.nav-link-logo
  font-size: 0

.nav-burger
  @media $breakpoint-xsmall
    display none

.nav-list
  list-style none
  padding-left 0
  line-height 1
  @media $breakpoint-xsmall
    display flex
  &__item
    padding: .5em 0
    @media $breakpoint-xsmall
      padding 0 1rem

.nav-link
  color var(--white)
  &:hover
    opacity 0.8
</style>
