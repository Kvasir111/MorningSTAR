<template>
  <div class="card">
    <ul>
      <li>{{clientName}}</li>
    </ul>
  </div>
</template>

<script>
    export default {
        name: "queueItem",
        props: ["repair"],
        data: function () {
            return {
                clientName: this.repair
            }
        }
    }
</script>

<style scoped>

</style>
