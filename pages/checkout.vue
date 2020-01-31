<template>
	<div class="h-screen flex">
		<div id="searchDiv" class="mx-auto w-full bg-black">
			<input type="text" class="rounded text-center" placeholder="Enter SO Number" v-on:keypress="search">
		</div>
		<div class="m-auto w-full md:w-2/3">
			<h1 class="text-2xl font-bold m-2">In progress repairs</h1>
			<div class="w-full">
				<div class="w-full" id="repairList" :key="index" v-for="(repair, index) in repairList">
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import queueItem from './queueItem';
	import firebase from '@/plugins/firebase'
    export default {
        name: 'checkout',
		data: function() {
        	return{
        		title: "Repair Checkout",
				repairList: [],
			}
		},
		async mounted() {
			//repairList is an array of repair objects that will be used to create the repair queue items
			await firebase
				.firestore()
				.collection("Finished Repairs")
				.get()
				//the snapshot is what the database looks like when the function is called
				.then(snapshot => {
					//a doc is essentially a record in firebase, each doc con contain literally anything, but in this case each one represents a repair item
					snapshot.forEach(doc => {
						this.repairList.push({
							//the doc ID will probably be used like a Service Order Number until I can come up with a better solution
							repairID: doc.id,
							//the data is 3 objects, customerObject, deviceObject, and repairObject, each one of them has some strings underneath it
							repairData: doc.data()
						});
						console.log(doc.data())
					})
				})
		},
		methods: {
        	search(searchID){
			}
		}
    };
</script>

<style scoped>

</style>
