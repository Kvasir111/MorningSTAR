<template>
<div>
	<span id='openButton' class="md:top-0" v-on:click="openNavigation">
		<left-arrow />
	</span>
	<div id="sideNavigation" class="navMenu inline-block h-screen">
		<span id="closeButton" v-on:click="closeNavigation" class="md:top-0">
			<arrow />
		</span>
		<div>
			<ul>
				<li :key="index" v-on:click="closeNavigation" v-for="(page, index) in links">
					<nuxt-link class="navButton text-white hover:text-black hover:bg-orange-500" v-bind:to="page.link">{{page.linkText}}</nuxt-link>
				</li>
			</ul>
		</div>
	</div>
</div>
</template>

<script>
    import Arrow from './arrow';
	import LeftArrow from './leftArrow';
	export default {
        name: 'navigation',
		components: { LeftArrow, Arrow },
		data:function() {
        	return{
				links: [
					{linkText: "Home", link: '/'},
					{linkText: "New Repair", link: "/new_repair"},
					{linkText: "Quick Fix", link: "/quickfix"},
					{linkText: "Repair Queue", link: "/queue"},
					{linkText: "Checkout", link: "/checkout"},
					{linkText: "Archive", link: '/archive'}
				],
			}
		},
		mounted() {
        document.getElementById("closeButton").style.display = 'hidden';
		},
		methods:{
        	openNavigation(){
				document.getElementById("sideNavigation").style.width = "250px";
				document.getElementById("closeButton").style.display = "block";

			},
			closeNavigation(){
				document.getElementById("sideNavigation").style.width = "0";
			}
		}
    };
</script>

<style scoped>

	.navButton {
		@apply block p-2;
		font-family: 'Montserrat', sans-serif;
	}
	.navMenu {
		@apply fixed bottom-0 right-0;
		background: #312F2F;
		height: 100%; /* 100% Full-height */
		width: 0; /* 0 width - change this with JavaScript */
		overflow-x: hidden; /* Disable horizontal scroll */
		z-index: 1;
		padding-top: 60px; /* Place content 60px from the top */
		transition: 0.25s; /* 0.5 second transition effect to slide in the sidenav */
	}
	.navMenu #closeButton{
		@apply bottom-0 right-0;
		position: absolute;
		font-size: 36px;
		margin-left: 50px;
	}
	#openButton{
		@apply absolute right-0 bottom-0;
	}
</style>
