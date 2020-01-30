<template>
  <div class="bg-white rounded w-1/3">
    <ul>
      <li>{{repair}}</li>
    </ul>
  </div>
</template>

<script>
    export default {
        name: "queueItem",
        props: ["repair"],
        data: function () {
            return {
                clientName: '',
            }
        },
        created() {
          console.log("created new item")
        }
    }
</script>

<style scoped>

</style>
