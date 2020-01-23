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
                clientName: this.repair['Customer Name'],
                accountNumber: this.repair['Account #'],
                serviceAddress: this.repair['Service Address'],
                inDate: this.repair['Date Checked in'],
            }
        }
    }
</script>

<style scoped>

</style>
