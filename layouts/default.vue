<template>
  <div>
    <nav
      class="navbar header has-shadow is-primary"
      role="navigation"
      aria-label="main navigation"
    >
      <div class="navbar-brand">
        <div class="navbar-burger">
          <span />
          <span />
          <span />
        </div>
      </div>
    </nav>

    <section class="main-content columns">
      <!-- <div class="container column"> -->
        <nuxt />
      <!-- </div> -->
    </section>
  </div>
</template>

<script>
export default {
  data () {
    return {

    }
  }
}
</script>

<style lang="scss">
.map-container {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
}
</style>