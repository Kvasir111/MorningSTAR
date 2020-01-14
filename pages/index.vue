<template>
  <div class="h-screen flex">
  <div class="m-auto bg-white rounded p-4">
    <ul class="">
      <nuxt-link class="homeLink hover:bg-gray-300 hover:text-white" to="/new_repair">New Repair</nuxt-link>
      <nuxt-link class="homeLink hover:bg-gray-300" to="/quick_fix">Quick Fix</nuxt-link>
      <nuxt-link class="homeLink hover:bg-gray-300" to="/repair_queue">Repair Queue</nuxt-link>
      <nuxt-link class="homeLink hover:bg-gray-300" to="/completed_repairs">Checkout Computer</nuxt-link>
    </ul>
  </div>
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
  .homeLink{
    @apply block text-center rounded p-2
  }

</style>
