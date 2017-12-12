<template> 
   <div class="question__wrap">
    <div class="question__timer">{{timeForReply}}</div>
   	<div class="question__text">{{x}} + {{y}} = ? </div>

   	<button class="question__answers" 
   	       v-for="answer in answers"
   	       v-on:click="onAnswer(answer)"
   	       > 
   	       {{answer}}
   </button>
   </div>
</template>


<script>
export default {
   props: ['settings'],
	 data() {
	 	return{
	 		 x: mtRand(this.settings.min , this.settings.max),
	 		 y: mtRand(this.settings.min , this.settings.max),
       timeForReply: this.settings.time,
       timerInterval: ' '
	 	}
	 },
   mounted: function () {
     
      this.timerInterval = setInterval(this.timer , 1000);
    
  },
  computed: {

      good() {
        return this.x + this.y;
      },

  	   answers(){

      var res = [this.good];


      while( res.length < this.settings.variants){
      	 var  num = mtRand( this.good- this.settings.range , this.good + this.settings.range);

      	 if ( res.indexOf(num) === -1) {
      	 	  res.push(num);
      	 }

      }

      return res.sort(function() {
      	   return Math.random() > 0.5;
      })

   }
      

 }, 
    methods: {
    	  onAnswer(num){
    	  	 if ( num === this.good) {
             this.$emit('succes');
    	  	 } else{
             this.$emit('error' , `${this.x} + ${this.y} = ${this.good}!`);
    	  	 } 
    	  } ,

        timer() {
          
          if(this.timeForReply > 1){
             this.timeForReply--; 
           } else{
             clearInterval(this.timerInterval)
             this.timeOut();
         }
        }, 
         timeOut() {
           this.$emit('timeOut' , `Время вышло!!! ${this.x} + ${this.y} = ${this.good}!`);
         }
        
   }

}






function mtRand(min , max) {
	 let diff = max - min;
	 return Math.floor(Math.random() * (diff + 1)) + min; 
}


	
</script>


<style>
   .question__wrap{
      min-height: 235px;
      background-color: #4DB6AC;
      border-radius: 4px;
      text-align: center;
      overflow: hidden;
      padding-bottom: 20px;
 }
 .question__timer{
  margin: 10px auto 0;
  font-size: 45px;
  font-weight: bold;
  color: #034777;
 }

  .question__text{
  	font-size: 20px;
  	margin: 15px auto 70px;

  }

  .question__answers{
  	 padding: 5px 15px;
  	 margin: 0 15px;
  	 background-color: #00c853;
  }

  .question__answers:hover{
  	 background-color: #00e676;
  }
	
</style>