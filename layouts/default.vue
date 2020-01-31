<template>
  <div class="">
	  <div class="mx-auto text-center">
		  <ul class="inline-flex" :key="index" v-for="(link, index) in links">
			  <li class="hover:bg-gray-400 nav-link"><nuxt-link v-bind:to=link.link>{{link.linkText}}</nuxt-link></li>
		  </ul>
	  </div>
    <nuxt />
  </div>
</template>

<script>
	export default {
		data : function() {
			return{
				links: [
					{linkText: "New Repair", link: "/new_repair"},
					{linkText: "Quick Fix", link: "/quickfix"},
					{linkText: "Repair Queue", link: "/queue"},
					{linkText: "Checkout", link: "/checkout"},
				],
			}
		}
	}
</script>
<style>
	.nav-link{
		@apply p-2 inline text-center bg-gray-600 rounded m-2
	}
	html{
		@apply bg-orange-600
	}
</style>
