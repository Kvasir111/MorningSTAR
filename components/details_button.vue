<template>
	<div class="bg-orange-800 px-2 text-white fontMont font-bold" v-on:click="rotate">
		{{text}}
		<svg  class="inline" xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 24 24" fill="none" v-bind:stroke="strokeColor" v-bind:stroke-width="width" stroke-linecap="round" stroke-linejoin="round">
			<path d="M6 9l6 6 6-6"/>
		</svg>
	</div>
</template>

<script>
    export default {
    	props: ['strokeColor', 'width', 'bgColor', 'text'],
        name: 'details_button',
		methods: {
    		rotate:{

			}
		}
    };
</script>

<style scoped>

</style>
