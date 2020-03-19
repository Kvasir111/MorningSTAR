<template>
	<div class="flex h-screen w-full">
		<resolution-card :key=index v-for="(penis, index) in rows" v-bind:repair="penis.repairData" v-bind:docID="penis.docID"></resolution-card>
	</div>
</template>

<script>
	import firebase from '@/plugins/firebase';
	import ResolutionCard from '../components/resolutionCard';
	import Close_repairButton from '../components/close_repairButton';

	export default {
		name: 'resolution',
		components: { Close_repairButton, ResolutionCard },
		data: function() {
			return {
				docID: '',
				rows: [],

				repair: {},
				//this is basically the only data member that's important to this page, it's the "what we did' bit
				repairResolution: '',

				//the local data members for the repair data
				//clientName: this.repair.Customer_Data['First Name'] + ' ' + this.repair.Customer_Data['Last Name']

			};
		},
		async mounted() {
			let d = {};
			 d = this.getURLVars()['SO'];
			console.log(d.id);
			let queueRef = firebase.firestore().collection('Repair Queue').doc(d);
			let getDoc = queueRef.get()
				.then(doc => {
					if (!doc.exists) {
						console.log('Invalid DocID');
					} else {
						console.log('Found Doc!');
						console.log(doc.data());
						let repairData = doc.data();
						let docID = doc.id;
						this.rows.push({repairData, docID})
					}
				})
				.catch(error => {
					console.log('Error Getting Doc: ', error);
				});

		},
		methods: {
			getCookie() {
				return document.cookie;
			},
			getURLVars(){
				let v = {};
				let parts = window.location.href.replace(/[?&]+([^=&]+)=([^&]*)/gi, function(m,key,value) {
					v[key] = value;
				});
				return v;
			}

		}
	};
</script>

<style scoped>
	h3 {
		@apply inline font-bold text-gray-700
	}

</style>
