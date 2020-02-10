<template>
<div>
	<span v-on:click="openNavigation">
		<arrow />
	</span>
	<div id="sideNavigation" class="navMenu inline-block h-screen">
		<span v-on:click="closeNavigation">
			<left-arrow class="closeButton" />
		</span>
		<ul>
			<li :key="index" v-on:click="closeNavigation" v-for="(link, index) in links" class="navButton text-white hover:bg-gray-300 hover:text-black">
				<nuxt-link v-bind:to="link.link" >{{link.linkText}}</nuxt-link>
			</li>
		</ul>
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
		methods:{
        	openNavigation(){
				document.getElementById("sideNavigation").style.width = "250px";

			},
			closeNavigation(){
				document.getElementById("sideNavigation").style.width = "0";
			}
		}
    };
</script>

<style scoped>

	.navButton {
		@apply block p-2
	}
	.navMenu {
		background: #312F2F;
		height: 100%; /* 100% Full-height */
		width: 0; /* 0 width - change this with JavaScript */
		position: fixed; /* Stay in place */
		z-index: 1; /* Stay on top */
		top: 0; /* Stay at the top */
		left: 0;
		overflow-x: hidden; /* Disable horizontal scroll */
		padding-top: 60px; /* Place content 60px from the top */
		transition: 0.5s; /* 0.5 second transition effect to slide in the sidenav */
	}
	.navMenu .closeButton{
		position: absolute;
		top: 0;
		right: 25px;
		font-size: 36px;
		margin-left: 50px;
	}

</style>
