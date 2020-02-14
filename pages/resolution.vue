<template>
    <div class="bg-white">
		<h1>{{repair}}</h1>
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
