<template>
	<div class="bg-white w-full rounded shadow-md p-2 mt-2 hover:shadow-lg card">
		<div id="quickDetails" class="block">
			<h1 class="font-bold fontMont">{{clientName}}</h1>
			<h2 class="fontMont italic font-bold text-gray-800" id="SO#">SO #:{{SONumber}}</h2>
			<ul id="">
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

		<div class="inline-block ">
			<button v-on:click="showDetails" v-bind:id="SOdetailButton" class="moreDetailsButton ">
				{{text}}
					<svg  class="inline" xmlns="http://www.w3.org/2000/svg"
						  width="30" height="30" viewBox="0 0 24 24" fill="none"
						  v-bind:stroke="arrowColor" v-bind:stroke-width="width" stroke-linecap="round" stroke-linejoin="round"
					v-bind:id="SOdetailsSVG">
						<path d="M6 9l6 6 6-6"/>
					</svg>
			</button>
		</div>
	</div>
</template>

<script>
	import firebase from '@/plugins/firebase'
	import Details_button from './details_button';
    export default {
        name: 'archive_item',
		components: { Details_button },
		props: ['repair'],
		data:function() {
			return{
				//button options
				arrowColor: "#fafafa",
				width: 3,
				text: 'More Details',
				//boolean to show or hide more details
				show: false,

				//this is the docID from firebase, it's used as the service order number
				SONumber: this.repair.repairID,

				//this is to uniquely ID the button for reference
				SOdetailButton: this.repair.repairID + "button",
				SOdetailsSVG: this.repair.repairID + "svg",
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
				let svg = document.getElementById(this.SOdetailsSVG);
				if (this.show === false) {
					//this is called when the "More Details" button is clicked, it sets the display of the hidden details to be shown, and also changes the button text to "less details"
					detailDiv.style.display = "inline";
					svg.style.transform = 'rotate(180deg)';
					this.text = "Less Details";
					this.show = true;
				} else if (this.show === true) {
					//Does the opposite of the above
					detailDiv.style.display = "none";
					svg.style.transform = 'rotate(0deg)';
					this.text = "More Details";
					this.show = false;
				}
			},
		}
    };
</script>

<style scoped>
	h3 {
		@apply inline font-bold text-gray-700
	}


</style>
