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
		<div v-bind:id="SONumber" class="hidden">
			<ul id="deviceInformation">
				<li><h3>Account#:</h3> {{accountNumber}}</li>
				<li><h3>Address:</h3> {{address}}</li>
			</ul>

			<ul id="repairInformation">
				<li><h3>Check in Date:</h3> {{checkInDate}}</li>
				<li><h3>Repair Data:</h3> {{checkInReason}}</li>
			</ul>
		</div>

		<div class="inline-block">
			<button type="button" v-bind:id="SONumber"
					class=" inline-block bg-orange-500 px-2 rounded text-white font-bold" v-on:click="showDetails">More
				Details
			</button>
			<button type="button" id="openSOButton" class="inline-block bg-red-500 px-2 rounded text-white font-bold">
				Open SO
			</button>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'queueItem',
		//the data from the firebase query is passed as an object, then parsed individually in the component
		props: ['repair'],
		data: function() {
			return {

				//boolean to show or hide more details
				show: false,

				//this is the docID from firebase, it's used as the service order number
				SONumber: this.repair.repairID,

				SOdetailButtons: this.repair.repairID + "button",

				//basic customer information, the first and last name come as separate data members but i've concatenated them here
				clientName: this.repair.repairData.Customer_Data['First Name'] + ' ' + this.repair.repairData.Customer_Data['Last Name'],
				accountNumber: this.repair.repairData.Customer_Data['Account #'],
				address: this.repair.repairData.Customer_Data['Address'],

				//device information, such as computer make and model
				deviceMake: this.repair.repairData.Device_Data['Make'],
				deviceModel: this.repair.repairData.Device_Data['Model'],

				//repair information, this is the description of the issue and when it was checked in, some of this might get moved to a different call since this can get lengthy if people are verbose
				checkInDate: this.repair.repairData.Repair_data['Check In Date'],
				checkInReason: this.repair.repairData.Repair_data['Check In Reason']
			};
		},
		created() {
			//for debugging, just logs the event into the console
			console.log('created new item');
		},
		methods: {
			showDetails() {
				let y = document.getElementById('detailsButton');
				let x = document.getElementById('moreDetails');
				if (this.show === false) {
					x.style.display = 'inline';
					y.innerHTML = 'Less Details';
					this.show = true;
				} else if (this.show === true) {
					x.style.display = 'none';
					y.innerHTML = 'More Details';
					this.show = false;
				}
			},
			copySO() {
			}
		}
	};
</script>

<style scoped>
	h3 {
		@apply inline italic
	}
	card{
		animation-duration: 1s;
		transition: max-height 1s ease-in-out;
	}

</style>
