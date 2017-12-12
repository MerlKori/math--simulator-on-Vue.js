<template> 
  <div class="start-screen__wrap">
  	<h3 class="start-screen__title">Вы готовы ?</h3>
  	<button class="start-screen__btn-start" v-on:click="$emit('onStart')">старт</button>
  </div>
</template>


<script>
  export default{
  	 methods: {
  	 	
  	 }
  }
	
</script>


<style scoped>
 
 .start-screen__wrap{
 	text-align: center;
 	background-color: #034777;
 	border-radius: 4px;
 	font-family: 'Open Sans', sans-serif;
  overflow: hidden;
 }

 .start-screen__title{
 	padding: 40px 0;
 	font-weight: 400;
 	font-size: 20px;
 	text-transform: uppercase;
 	color: #fff;
 }

 .start-screen__btn-start{
 	
 	margin: 20px 0 35px;
 	background-color: #BE980F;
 }

 .start-screen__btn-start:hover{
 	background-color: #EDBE13;
 }

	
</style>