<template>
	<div class="h-screen flex">
		<form class="md:m-auto w-10/12 mx-auto md:w-2/3" v-on:submit="createNewSO">
			<div>
				<h1 class="font-bold text-xl">New Check-In</h1>
				<h1 class="italic">Enter Details for new repair</h1>
			</div>
			<div class="bg-white rounded-lg p-4 text-center shadow-lg mb-2" id="Customer Information Block">
				<h2 class="mb-2 fontMont">Enter Customer Information</h2>
				<div class="flex-wrap overflow-hidden">
					<input :key=index v-for="(key, index) in customerInformation"
						   class="formTextInput focus:outline-none border-2 border-transparent focus:border-orange-500 mx-2 my-2 text-center w-full lg:w-1/3"
						   v-bind:id="customerInformation[index].text"
						   v-bind:placeholder="customerInformation[index].text"
						   v-model="customerInformation[index].value">
				</div>

				<div id="Computer Information Block" class="text-center p-2 ">
					<h2 class="fontMont mb-2">Enter Computer Information</h2>
					<div class="align-middle flex-wrap overflow-hidden">
						<select v-model="deviceInformation[0].value" class="focus:outline-none border-2 border-transparent focus:border-orange-500  formTextInput mx-2 my-2 text-center w-full md:w-auto"
								id="MFG Selection">
							<option disabled selected>Select MFG</option>
							<option :key="index" v-model="deviceInformation[0].value" v-for="(oem, index) in mfgs">
								{{oem}}
							</option>
						</select>
						<input type="text"
							   class="focus:outline-none formTextInput border-2 border-transparent focus:border-orange-500  mx-2 my-2 text-center w-full md:w-auto"
							   v-model="deviceInformation[1].value" v-bind:placeholder="deviceInformation[1].text">
						<input type="text"
							   class="focus:outline-none formTextInput border-2 border-transparent focus:border-orange-500  mx-2 my-2 text-center w-full md:w-auto"
							   v-model="deviceInformation[2].value" v-bind:placeholder="deviceInformation[2].text">
					</div>
				</div>
				<div id="issue description" class="text-center">
					<textarea cols="50" rows=10 v-model="issue" class="myTextArea border-2 border-transparent focus:border-orange-500 "
							  placeholder="Description of issues"></textarea>
				</div>
				<div id="pricing options">
					<select v-model="repairType" required class="focus:outline-none border-2 border-transparent focus:border-orange-500 formTextInput mx-2 my-2 text-center w-full md:w-auto">
						<option selected disabled>Select Pricing Option</option>
						<option :key="index" v-for="(price, index) in prices">
							{{price.type}} {{price.cost}}
						</option>
					</select>
				</div>
				<div class="text-center">
					<button type="submit" class="formButton">Create New Repair</button>
				</div>
			</div>

		</form>
	</div>
</template>

<script>
	import firebase from '@/plugins/firebase';

	export default {
		name: 'new_repair',
		data: function() {
			return {
				//this object holds the basic contact information for the customer
				customerInformation: [
					{ text: 'First Name', value: '' },
					{ text: 'Last Name', value: '' },
					{ text: 'Address', value: '' },
					{ text: 'Account #', value: '' },
					{ text: 'Phone Number', value: '' },
					{ text: 'Email', value: '' }
				],
				//an array of PC MFGs, this powers the drop down
				mfgs: ['Alienware', 'Apple', 'Custom Build', 'Dell', 'Gateway', 'HP', 'Lenovo', 'MSI', 'Other Official OEM', 'Sony', 'Toshiba', 'eMachine'],
				//This object holds the basic computer information, make and model, uses the above array as it's data source
				deviceInformation: [
					{ text: 'Make', value: '' },
					{ text: 'Model Number', value: '' },
					{ text: 'Serial Number', value: '' }
				],
				//just a long ass string about what's wrong with the PC
				issue: '',
				//literally the date it was dropped off
				checkInDate: '',

				//pricing options
				prices: [
					{type: "Standard 1hr Labor", cost: '$70'},
					{type: "PC Build", cost: '$100'},
					{type: "Misc Hardware Install", cost: '$25'},
					{type: "Misc Software Install/Fix", cost: '$25'},
				],

				repairType: '',
			};
		},
		methods: {
			createNewSO() {
				//I'll have to make some function to create a unique SO number, but for now it's set at 1
				//calls the create function to make an array of objects to send to the database
				let serviceOrder = this.createServiceOrderObject();

				//instantiates the firestore
				const database = firebase.firestore();

				database.collection('Repair Queue').add(serviceOrder).then(function(docref) {
					//logs the docid to the console for reference
					console.log('Created new SO with doc ID of: ' + docref.id);
				});
			},
			createServiceOrderObject() {

				//this function will create 3 objects based off the data declarations in the page, then it returns the  data as an object with 3 objects
				//the 3 objects here use non-standard naming because it makes it easier to read in firebase
				let Customer_Data = {
					'First Name': this.customerInformation[0].value,
					'Last Name': this.customerInformation[1].value,
					'Address': this.customerInformation[2].value,
					'Account #': this.customerInformation[3].value,
					'Phone Number': this.customerInformation[4].value
				};

				let Device_Data = {
					'Make': this.deviceInformation[0].value,
					'Model': this.deviceInformation[1].value,
					'Serial Number': this.deviceInformation[2].value
				};

				let today = new Date();
				let dd = String(today.getDate()).padStart(2, '0');
				let mm = String(today.getMonth() + 1).padStart(2, '0'); //January is 0!
				let yyyy = today.getFullYear();

				today = mm + '/' + dd + '/' + yyyy;
				let Repair_data = {
					'Check In Reason': this.issue,
					'Check In Date': today,
					'Quoted Price' : this.repairType,
				};
				//returns the 3 objects back to the createNewSO function to send off to firebase
				return {
					Customer_Data, Device_Data, Repair_data
				};
			}
		}
	};
</script>

<style scoped>
	.formTextInput {
		@apply rounded-full bg-gray-200 p-2
	}

	.formButton {
		@apply bg-green-400 px-4 py-2 rounded-full mx-auto;
		font-family: 'Montserrat', sans-serif;
	}

	h2 {
		@apply w-full border-b-2 border-gray-500
	}

	h1 {
		font-family: 'Montserrat', sans-serif;
	}

	.fontMont {
		font-family: 'Montserrat', sans-serif;
	}
	.myTextArea {
		@apply w-full border-2 rounded-lg p-2 bg-gray-200 outline-none
	}

</style>
