<template>
	<div class="flex h-screen w-full">
		<div class="bg-white rounded-lg w-10/12 md:w-2/3 shadow-lg mx-auto m-4">
			<div class="text-center mx-auto">
				<h1 class="fontMont text-2xl">Repair Resolution</h1>
			</div>
			<div class="block p-2" id="Customer Block">
				<h1 class="fontMont font-bold">{{repair.Customer_Data['First Name']}} {{repair.Customer_Data['Last Name']}}</h1>
				<h2 class="fontMont italic font-bold text-gray-800">SO#: {{docID}}</h2>
				<h2 class="fontMont">Contact: {{repair.Customer_Data['Phone Number']}}</h2>
				<h2 class="fontMont">Account #: {{repair.Customer_Data['Account #']}}</h2>
			</div>
			<div class="block p-2" id="Problem Block">
				<h1 class="fontMont font-bold text-xl border-b-2 border-black">Repair Details</h1>
				<h2 class="text-xl mt-4">Original Issue</h2>
				<h2 class="fontMont text-gray-800">Original Check-In Date: {{repair.Repair_data['Check In Date']}}</h2>
				<p id="Check-in reason" class="fontMont text-red-500">{{repair.Repair_data['Check In Reason']}}</p>
				<label class="hidden" for="Resolution">Repair Resolution</label>
				<textarea rows="6" v-model="repairResolution" class="myTextArea" id="Resolution" placeholder="Enter Repair Resolution"/>
			</div>
			<div  class="flex w-full justify-end content-center" id="Button Block">
				<button class="greenButton" v-on:click="markCompleted(docID)">
					Close Repair
					<Close_repairButton class="inline" stroke-color="#fafafa" width="3"/>
				</button>
			</div>
		</div>
	</div>
</template>

<script>
	import firebase from "@/plugins/firebase"
	import Close_repairButton from './close_repairButton';
    export default {
    	props: ['repair', 'docID'],
        name: 'resolutionCard',
		components: { Close_repairButton },
		data : function() {
			return{
				repairResolution: '',

			}
		},
		methods:{
			addResolution(doc){
				//this takes in a doc item and adds a new member underneath the "Repair_data" member with what we did
				doc.Repair_data['Resolution'] = this.repairResolution;
				return doc;
			},
			markCompleted(id){

				console.log(id);
				//moves the doc from the repair queue into the "Finished Repairs" collection

				//gets the reference for the collection of in progress repairs, using the id that was passed to it
				let docRef = firebase.firestore().collection("Repair Queue").doc(id);
				//actually gets the doc and does something with it
				docRef.get()
					.then(doc =>{
						if (!doc.exists){
							console.log("404 doc not found");
						}
						else{
							console.log("Found Document!");
							let old = doc.data();
							//this calls a function to add the "what we did" bit to the doc before it's moved to the "Finished Repairs"
							old = this.addResolution(old);
							//Copies the doc to the new collection
							firebase.firestore().collection("Finished Repairs").add(old);
							console.log("Moved new Document");
							//removes the doc from the repair queue, there is no "Move" function, so it has to essentially be copy pasted into the new collection, then removed from the old
							firebase.firestore().collection("Repair Queue").doc(id).delete();
							console.log("Removed the old doc");
							//this pushes the user into the "checkout" page
							window.location = '/checkout'
						}
					}).catch(error =>{
					console.log("Something went wrong....", error)
				})
				//let finished = firebase.firestore.collection("Finished Repairs");
			}
		}

    };
</script>

<style scoped>

</style>
