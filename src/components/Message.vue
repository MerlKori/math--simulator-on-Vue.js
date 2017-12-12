<template> 
<div class="message__wrap " v-bind:class=" 'wrap-' + type ">
	 <h3 class="message__title">{{ text }}</h3>
	 <button class="message__btn-continue" 
    v-on:click="$emit('onNext')"
    > 
   Продолжить 
   </button>
</div>
</template>


<script>
	   export default {
	   	 props: ['text' , 'type']
	   }
</script>


<style>

  .message__wrap{
       min-height: 235px;
  	   border-radius: 4px;
  	   text-align: center;
       overflow: hidden;
  }

  .wrap-succes{
  	   background-color: #b9f6ca;
  }

  .wrap-error{
  	   background-color: #ff9e80;
  }

  .message__title{
     margin: 60px auto 80px;
  	 font-size: 20px;
     font-weight: 400;
  	 color: #000;
  }
	
</style>