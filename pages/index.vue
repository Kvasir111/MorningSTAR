<template>
  <div class="h-screen flex">
  <div class="m-auto w-full">
	  <img v-bind:src="logo" alt="morningSTAR logo">
  </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  data: function() {
	return{
		logo: require('../assets/morningStar.svg'),
	}
  }
}
</script>

<style>
  .homeLink{
    @apply block text-center rounded p-2
  }

</style>
