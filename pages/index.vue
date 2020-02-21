<template>
	<div class="h-screen flex">
		<script src="node_modules/firebaseui/dist/firebaseui.js"></script>
		<link type="text/css" rel="stylesheet" href="node_modules/firebaseui/dist/firebaseui.css" />
		<div class="mt-4 md:m-auto w-full">
			<img v-bind:src="logo" alt="morningSTAR logo">
			<div class="text-center w-full block md:flex justify-center">
				<nuxt-link :key="index" class="homeLink md:w-1/6 mx-auto block hover:bg-black hover:text-orange-500"
						   v-for="(link, index) in links" v-bind:to="link.link">{{link.linkText}}
				</nuxt-link>
			</div>
		</div>
	</div>
</template>

<script>
	import Logo from '~/components/Logo.vue';

	export default {
		components: {
			Logo
		},
		mounted() {
		},
		data: function() {
			return {
				logo: require('../assets/morningStar.svg'),

				links: [
					{ linkText: 'New Repair', link: '/new_repair' },
					{ linkText: 'QuickFix', link: '/quickfix' },
					{linkText: 'Repair Queue', link: '/queue'},
					{linkText: 'Checkout', link: '/checkout'}
				]
			};
		}
	};
</script>

<style>
	.homeLink {
		@apply bg-white px-4 m-2 py-2 text-xl rounded-lg;
		font-family: 'Montserrat', sans-serif;
	}

</style>
