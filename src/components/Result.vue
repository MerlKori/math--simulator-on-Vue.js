<template> 
<div class="result__wrap">
	 <h2 class="result__title">Ваш результат</h2>
	 <h3 class="answers answers--green">Правильных ответов - {{stats.succes}}</h3>
	 <h3 class="answers answers--red">Неправильных ответов - {{stats.error}}</h3>
	 <hr>

	 <button 
	 class="result__btn"  
	 v-on:click="$emit('onStart')"
	 >Повторить</button>
	 <button 
	 class="result__btn"
   v-on:click="$emit('onNextLevel')"
	 >Следующий уровень</button>
</div>
</template>


<script>
	    export default {
	   	 props: ['stats']
	   }
</script>


<style>

 .result__wrap{
 	   min-height: 235px;
 	   padding: 0 20px;
 	   background-color: #034777;
 	   border-radius: 4px;
     text-align: center;
     overflow: hidden;
 }

 .result__title{
 	font-weight: 400;
 	color: #DE9D1A;
 }

 .answers{
 	  text-align: left;
 	  font-weight: 400;
 	  margin: 10px auto;
 	  
 }

 .answers--red{
 	  color: #DE2909;
 }

 .answers--green{
 	  color: #3FB07D;
 }

 hr{
 	margin-bottom: 40px;
 }

 .result__btn{
 	 margin: 0 10px;
 	 background-color: #BE980F;
 }

 .result__btn:hover{
 	background-color: #EDBE13;
 }




	
</style>