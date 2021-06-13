<template>
  <div>
    <slot>
      <button type="button" class="burger" title="Toggle menu">
        <span class="burger__bar"></span>
        <span class="burger__bar"></span>
      </button>
    </slot>
  </div>
</template>

<script>
export default {};
</script>

<style lang="stylus" scoped>
.burger
  cursor pointer
  position relative
  height 1.1rem
  width 1.5rem
  display block
  z-index 9
  border 0
  border-radius 0
  background-color transparent
  pointer-events all
  transition transform var(--default-transition-duration--2) var(--bezier-transition-function)

  .nav-opened &
    transform rotate(-180deg)
    .burger
      &__bar
        &:first-child
          transform rotate(-45deg)
        &:last-child
          transform rotate(45deg)

  &__bar
    position: absolute
    background-color: var(--white)
    top 50%
    right 0
    left 0
    width 1.5rem
    height 2px
    margin -1px auto 0
    transition: transform var(--default-transition-duration--2) var(--bezier-transition-function),
      opacity var(--default-transition-duration) var(--bezier-transition-function),
      background-color var(--default-transition-duration--2) var(--bezier-transition-function);
    &:first-child
      transform translateY(-4px)
    &:last-child
      transform translateY(4px)
</style>
