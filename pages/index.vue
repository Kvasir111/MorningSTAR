<template>
  <div>
    <ul>
      <nuxt-link to="/new_repair">New Repair</nuxt-link>
      <nuxt-link to="/quick_fix">Quick Fix</nuxt-link>
      <nuxt-link to="/repair_queue">Repair Queue</nuxt-link>
      <nuxt-link to="/completed_repairs">Checkout Computer</nuxt-link>
    </ul>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  }
}
</script>

<style>

</style>
