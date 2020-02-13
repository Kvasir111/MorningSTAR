<template>
	<svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 24 24" fill="none" v-bind:stroke="strokeColor" v-bind:stroke-width="width" stroke-linecap="round" stroke-linejoin="round">
		{{text}}
		<path d="M20 6L9 17l-5-5"/>
	</svg>
</template>

<script>
    export default {
		props: ['strokeColor', 'width', 'text'],
        name: 'close_repairButton'
    };
</script>

<style scoped>

</style>
