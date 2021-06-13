<template>
  <div>
    <section-primary-nav />

    <nuxt />
  </div>
</template>

<script>
export default {
  components: {},
};
</script>

<style lang="stylus">
// Accessible/SEO friendly CSS hiding
.sr-only
  position absolute
  height 1px
  width 1px
  overflow hidden
  clip rect(1px, 1px, 1px, 1px)

// https://nuxtjs.org/examples/transitions
.page-enter-active
  transition opacity 0.25s ease-out
.page-leave-active
  transition opacity 0.25s ease-out

.page-enter,
.page-leave-to
  opacity 0
</style>
