<template>
	<div class="flex h-screen w-full">
    <div class="bg-white rounded-lg w-10/12 shadow-lg mx-auto m-4">
		<h1>{{repair}}</h1>
	</div>
	</div>
</template>

<script>
	import firebase from '@/plugins/firebase';
	import ResolutionCard from '../components/resolutionCard';
    export default {
        name: 'resolution',
		components: { ResolutionCard },
		data: function(){
        	return{
        		docID: '',
				repair: {},
			}
		},
		async mounted() {
        	let id = this.getCookie();
        	console.log(id);
        	let queueRef = firebase.firestore().collection('Repair Queue').doc(id);
			let getDoc = queueRef.get()
			.then(doc =>{
				if (!doc.exists){
					console.log("Invalid DocID")
				}
				else {
					console.log("Found Doc!");
					console.log(doc.data());
					this.repair = doc.data();
					this.docID = doc.id;
				}
			})
			.catch(error =>{
				console.log("Error Getting Doc: ", error)
			})

		},
		methods: {
        	getCookie(){
        		return  document.cookie;
			}
		}
	};
</script>

<style scoped>


</style>
