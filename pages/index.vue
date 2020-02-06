<template>
  <div class="h-screen flex">
  <div class="m-auto w-full">
	  <img src="@/assets/morningstar.svg" alt="morningSTAR logo">
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
