<template>
    <div>
	</div>
</template>

<script>
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

				//device information, such as computer make and model
				deviceMake: this.repair.repairData.Device_Data['Make'],
				deviceModel: this.repair.repairData.Device_Data['Model'],

				//repair information, this is the description of the issue and when it was checked in, some of this might get moved to a different call since this can get lengthy if people are verbose
				checkInDate: this.repair.repairData.Repair_data['Check In Date'],
				checkInReason: this.repair.repairData.Repair_data['Check In Reason']
			}
		}
    };
</script>

<style scoped>

</style>
