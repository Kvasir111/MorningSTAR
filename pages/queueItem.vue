<template>
  <div class="bg-gray-300 hover:bg-orange-500 rounded w-full shadow-lg p-2">
    <ul id="customerInformation">
      <li><h3>Customer Name:</h3> {{clientName}}</li>
      <li><h3>Account#:</h3> {{accountNumber}}</li>
      <li><h3>Address:</h3> {{address}}</li>
    </ul>

    <ul id="deviceInformation">
      <li><h3>Computer Make:</h3> {{deviceMake}}</li>
      <li><h3>Model #:</h3> {{deviceModel}}</li>
    </ul>

    <ul id="repairInformation">
      <li><h3>Check in Date:</h3> {{checkInDate}}</li>
      <li><h3>Repair Data:</h3> {{checkInReason}}</li>
    </ul>
  </div>
</template>

<script>
    export default {
        name: "queueItem",
      //the data from the firebase query is passed as an object, then parsed individually in the component
        props: ["repair"],
        data: function () {
            return {

              //basic customer information, the first and last name come as separate data members but i've concatenated them here
              clientName: this.repair.repairData.customerObject["First Name"] + ' ' + this.repair.repairData.customerObject["Last Name"],
              accountNumber: this.repair.repairData.customerObject['Account #'],
              address: this.repair.repairData.customerObject['Address'],

              //device information, such as computer make and model
              deviceMake: this.repair.repairData.deviceObject["Make"],
              deviceModel: this.repair.repairData.deviceObject["model"],

              //repair information, this is the description of the issue and when it was checked in, some of this might get moved to a different call since this can get lengthy if people are verbose
              checkInDate: this.repair.repairData.repairObject["Check In Date"],
              checkInReason: this.repair.repairData.repairObject["Check In Reason"]
            }
        },
        created() {
          //for debugging, just logs the event into the console
          console.log("created new item");
        }
    }
</script>

<style scoped>
  h3{
    @apply inline italic
  }

</style>
