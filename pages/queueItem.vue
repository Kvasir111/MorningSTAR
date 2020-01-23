<template>
  <div class="card">
    <ul>
      <li>{{clientName}}</li>
      <li>{{accountNumber}}</li>
      <li>{{serviceAddress}}</li>
      <li>{{inDate}}</li>
    </ul>
  </div>
</template>

<script>
    export default {
        name: "queueItem",
        props: ["repair"],
        data: function () {
            return {
                clientName: this.repair.customerObject['First Name'] + this.repair.customerObject['Last Name'],
                accountNumber: this.repair.customerObject['Account #'],
                serviceAddress: this.repair.customerObject['Address'],
                inDate: this.repair.customerObject['Check In Date'],
            }
        }
    }
</script>

<style scoped>

</style>
