<template>
	<div class="h-screen flex">
		<div class="mx-auto w-10/12 md:w-2/3">
			<h1 class="text-2xl font-bold m-2 text-center">{{title}}</h1>
			<div class="w-full">
				<div class="w-full" id="repairList" :key="index" v-for="(repair, index) in repairList">
					<archive_item v-bind:repair="repair"></archive_item>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import firebase from '@/plugins/firebase'
	import Archive_item from '../components/archive_item';
	export default {
        name: 'archive',
		components: { Archive_item },
		data:function() {
			return{
				title: "Repair Archive",
				repairList: [],
			}
		},
		async mounted() {
			//repairList is an array of repair objects that will be used to create the repair queue items
			await firebase
				.firestore()
				.collection("Archive")
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
	};
</script>

<style scoped>

</style>
