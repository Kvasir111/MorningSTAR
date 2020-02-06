<template>
  <div>
	  <navigation />
    <nuxt />
  </div>
</template>

<script>
	import Navigation from '../components/navigation';
	export default {
		components: { Navigation },
		data : function() {
			return{

			}
		}
	}
</script>
<style>
	html{
		@apply bg-orange-600
	}
</style>
