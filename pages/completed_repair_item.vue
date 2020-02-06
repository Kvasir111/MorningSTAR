<template>
	<div class="bg-white w-full rounded shadow-md p-2 mt-2 hover:shadow-lg card">
		<div id="quickDetails" class="block">
			<h1 class="italic font-bold" id="SO#" v-on:click="copySO">SO #:{{SONumber}}</h1>
			<ul id="">
				<li><h3>Customer Name:</h3> {{clientName}}</li>
				<li><h3>Make:</h3> {{deviceMake}}</li>
				<li><h3>Model #:</h3> {{deviceModel}}</li>
			</ul>

		</div>
		<div v-bind:id="SOdetails" class="hidden">
			<ul id="More Customer Information">
				<li><h3>Phone#:</h3> {{phoneNumber}}</li>
				<li><h3>Account#:</h3> {{accountNumber}}</li>
				<li><h3>Address:</h3> {{address}}</li>
			</ul>

			<ul id="repairInformation">
				<li><h3>Check in Date:</h3> {{checkInDate}}</li>
				<li><h3>Repair Data:</h3> {{checkInReason}}</li>
			</ul>
		</div>

		<div class="inline-block">
			<button type="button" v-bind:id="SOdetailButton"
					class=" inline-block bg-orange-500 px-2 rounded text-white font-bold" v-on:click="showDetails">More
				Details
			</button>
			<button type="button" v-bind:id="closeRepairButton" class=" inline-block bg-red-500 px-2 rounded text-white font-bold" v-on:click="markCompleted(SONumber)">
				Checkout Repair
			</button>
		</div>
	</div>
</template>

<script>
	import firebase from '@/plugins/firebase'
    export default {
    	props: ['repair'],
        name: 'completed_repair_item',

		data:function() {
			return{
				//boolean to show or hide more details
				show: false,

				//this is the docID from firebase, it's used as the service order number
				SONumber: this.repair.repairID,

				//this is to uniquely ID the button for reference
				SOdetailButton: this.repair.repairID + "button",
				SOdetails: this.repair.repairID + "div",
				closeRepairButton: this.repair.repairID + "close",

				//basic customer information, the first and last name come as separate data members but i've concatenated them here
				clientName: this.repair.repairData.Customer_Data['First Name'] + ' ' + this.repair.repairData.Customer_Data['Last Name'],
				accountNumber: this.repair.repairData.Customer_Data['Account #'],
				address: this.repair.repairData.Customer_Data['Address'],
				phoneNumber : this.repair.repairData.Customer_Data['Phone Number'],

				//device information, such as computer make and model
				deviceMake: this.repair.repairData.Device_Data['Make'],
				deviceModel: this.repair.repairData.Device_Data['Model'],

				//repair information, this is the description of the issue and when it was checked in, some of this might get moved to a different call since this can get lengthy if people are verbose
				checkInDate: this.repair.repairData.Repair_data['Check In Date'],
				checkInReason: this.repair.repairData.Repair_data['Check In Reason']
			}
		},
		methods:{
			showDetails() {
				let detailDiv = document.getElementById(this.SOdetails);
				let button = document.getElementById(this.SOdetailButton);
				if (this.show === false) {
					//this is called when the "More Details" button is clicked, it sets the display of the hidden details to be shown, and also changes the button text to "less details"
					detailDiv.style.display = "inline";
					button.innerHTML = "Less Details";
					this.show = true;
				} else if (this.show === true) {
					//Does the opposite of the above
					detailDiv.style.display = "none";
					button.innerHTML = "More Details";
					this.show = false;
				}
			},
			copySO() {
			},
			markCompleted(id){
				console.log(id);
				//moves the doc from the repair queue into the "Finished Repairs" collection

				//gets the reference for the collection of in progress repairs, using the id that was passed to it
				let docRef = firebase.firestore().collection("Finished Repairs").doc(id);
				//actually gets the doc and does something with it
				docRef.get()
					.then(doc =>{
						if (!doc.exists){
							console.log("404 doc not found");
						}
						else{
							console.log("Found Document!");
							let old = doc.data();
							firebase.firestore().collection("Archive").add(old);
							console.log("Moved new Document");
							firebase.firestore().collection("Finished Repairs").doc(id).delete();
							console.log("Removed the old doc")
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
	h3 {
		@apply inline italic
	}

</style>
