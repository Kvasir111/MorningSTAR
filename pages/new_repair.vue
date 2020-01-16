<template>
	<div class="h-screen flex">
    <form class="md:m-auto w-full md:w-1/3" v-on:submit="">
      <div class=" m-auto bg-gray-300 p-2 rounded-t ">
        <h1>New Check-In</h1>
        <h1>Enter Details for new repair</h1>
      </div>
      <div class="bg-white rounded-b p-4">
        <h2>Enter Customer Information</h2>
      <div class="text-center" :key=index v-for="(key, index) in customerInformation" id="Customer Information Block">
        <input class="formTextInput focus:outline-none" v-bind:id="customerInformation[index].text" v-bind:placeholder="customerInformation[index].text" v-model="customerInformation[index].value">
      </div>
      <div id="Computer Information Block" class="text-center p-2 ">
        <h2>Enter Computer Information</h2>
        <select class="focus:outline-none formTextInput" id="MFG Selection">
          <option disabled selected>Select MFG</option>
          <option :key="index" v-model="deviceInformation[0].value" v-for="(oem, index) in mfgs">{{oem}}</option>
        </select>
        <input type="text" class="focus:outline-none formTextInput" v-model="deviceInformation[1].value" v-bind:placeholder="deviceInformation[1].text">
      </div>
      <div id="issue description" class="text-center">
        <textarea cols="50" v-model="issue" class="w-full border-2 border-gray-400" placeholder="Description of issues"></textarea>
      </div>
        <div class="text-center">
        <button type="submit" class="formButton">Create New Repair</button>
        </div>
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
        },
        methods :{
          createNewSO(){
            console.log("Working!")
          }
        }
    }
</script>

<style scoped>
  .formTextInput{
    @apply border-gray-400 border-b-2 p-2
  }
  .formButton{
    @apply bg-gray-400 px-4 py-2 rounded mx-auto
  }
  h2{
    @apply w-full border-b-2 border-gray-500
  }

</style>
