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

        data : function(){
            return{
            }
        },

        async asyncData(){
            //repairList is an array of repair objects that will be used to create the repair queue items
          let repairList = [];
          await firebase
              .firestore()
              .collection("Repair Queue")
              .get()
              //the snapshot is what the database looks like when the function is called
              .then(snapshot =>{
                  //a doc is essentially a record in firebase, each doc con contain literally anything, but in this case each one represents a repair item
                  snapshot.forEach(doc =>{
                      repairList.push({
                          //the doc ID will probably be used like a Service Order Number until I can come up with a better solution
                          repairID: doc.id,
                          //the data is 3 objects, customerObject, deviceObject, and repairObject, each one of them has some strings underneath it
                          repairData: doc.data()
                      })
                  })
              })
        },

        created() {
            //fetches all the in progress tickets when the page is created
            //this.fetchRepairs()
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
                        //pushes the list of docs into the "list"
                        this.list.push(doc);
                    })
                })
            },
        }
    };
</script>

<style scoped>

</style>
