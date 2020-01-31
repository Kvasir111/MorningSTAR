<template>
    <div>
      <h1>Service sssOrder</h1>
    </div>
</template>

<script>
    export default {
        name: '_serviceorder',

		data : function() {
        	return{
        		id: this.$route.params.SOnumber,
			}
		}
    };
</script>

<style scoped>

</style>
