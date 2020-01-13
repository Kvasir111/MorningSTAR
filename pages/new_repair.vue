<template>
	<div class="h-screen flex">
    <form class="m-auto">
      <div :key=index v-for="(key, index) in customerInformation" id="Customer Information Block">
        <input v-bind:id="customerInformation[index].text" v-bind:placeholder="customerInformation[index].text" v-model="customerInformation[index].value">
      </div>
      <div id="Computer Information Block">
        <select id="MFG Selection">
          <option disabled>Select MFG</option>
          <option :key="index" v-model="deviceInformation[0].value" v-for="(oem, index) in mfgs">{{oem}}</option>
        </select>
        <input type="text" v-model="deviceInformation[1].value" v-bind:placeholder="deviceInformation[1].text">
      </div>
      <div id="issue description">
        <textarea cols="50" v-model="issue" placeholder="Description of issues"></textarea>
      </div>
    </form>
  </div>
</template>

<script>
    export default {
        name: "new_repair",
        data : function () {
            return{
                //this object holds the basic contact information for the customer
                customerInformation: [
                    {text: 'First Name', value: ''},
                    {text: 'Last Name', value: ''},
                    {text: 'Address', value: ''},
                    {text: 'Account #', value: ''},
                    {text: 'Phone Number', value: ''},
                ],
                //an array of PC MFGs, this powers the drop down
                mfgs: ['Dell', 'HP', 'Gateway', 'Toshiba', 'Lenovo', 'Alienware', 'MSI', 'Custom Build'],
                //This object holds the basic computer information, make and model, uses the above array as it's data source
                deviceInformation: [
                    {text: 'Make', value: ''},
                    {text: 'Model Number', value: ''},
                    {text: 'Serial Number', value: ''}
                ],
                //just a long ass string about what's wrong with the PC
                issue: '',
                //literally the date it was dropped off
                checkInDate: ''
            }
        }
    }
</script>

<style scoped>

</style>
