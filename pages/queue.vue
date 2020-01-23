<template>
	<div class="h-screen flex">
    <div class="m-auto w-1/3">
      <div class="bg-gray-400 rounded-t">
        <h1>In progress repairs</h1>
      </div>
      <div class="bg-white rounded-b">
        <div id="repairList">

        </div>
      </div>
    </div>
  </div>
</template>

<script>
    import firebase from '@/plugins/firebase';
    import Vue from 'vue';
    import queueItem from './queueItem';
    export default {
        name: 'queue',

        created() {
            //fetches all the in progress tickets when the page is created
            this.fetchRepairs()
        },
        methods: {
            fetchRepairs(){
                const database = firebase.firestore();

                //gets the collection of in progress repairs
                const repairsRef = database.collection('Repair Queue');

                let allRepairs = repairsRef.get().then(snapshot =>{
                    //the snapshot is basically just that, what the database looks like when the function is called
                    snapshot.forEach(doc =>{


                        console.log(doc.data());
                        //appends a new repair to the repair list
                        //this.appendToList(doc.data, doc.id)
                    })
                })
            },
            appendToList(repairData, repairID){
                let ComponentClass = Vue.extend(queueItem);
                let instance = new ComponentClass({
                    propsData: {repairData}
                });

                instance.$mount();
                this.$refs.repairList.appendChild(instance.$el);
            }
        }
    };
</script>

<style scoped>

</style>
