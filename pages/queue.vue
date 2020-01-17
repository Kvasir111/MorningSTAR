<template>
	<div class="h-screen flex">
    <div class="m-auto w-1/3">
      <div class="bg-gray-400 rounded-t">
        <h1>In progress repairs</h1>
      </div>
      <div class="bg-white rounded-b">
        <div :key="index" v-for="(repair, index) in repairQueue">

        </div>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        name: 'queue'

    };
</script>

<style scoped>

</style>
