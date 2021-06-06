<template>
  <div>
    <nav-menu></nav-menu>
    <router-view/>
  </div>
</template>

<script>
  import NavMenu from './comon/NavMenu'
  export default {
    name: 'Home',
    components: {NavMenu}
  }
</script>

<style scoped>

</style>

