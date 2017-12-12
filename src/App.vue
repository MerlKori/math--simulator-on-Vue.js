<template>
  <div class="traning">
    <h1>Математический тренажер</h1>
    <h2 class="traning__subtitle">Уровень - {{level + 1}} </h2>
    <div class="progressbar">
      <div class="progressbar__load-line" :style="progressStyles"></div>
    </div>
    
    <div class="box">
      <transition name="flip" mode="out-in">  
    <AppStartScreen 
       v-if="state == 'start'"
       @onStart="onStart"
    > </AppStartScreen>

    <AppQuestion 
       v-else-if="state == 'quest'"
       @succes="onSucces"
       @error="onError"
       @timeOut="ontimeOut"
       v-bind:settings="levels[level]"
       >

     </AppQuestion>
    <AppMessage v-else-if="state == 'msg'"
                v-bind:text="message.text"
                v-bind:type="message.type"
                @onNext="onNext"

    > </AppMessage>
    <AppResult v-else-if="state == 'result'"
               v-bind:stats="stats"
               @onStart="onStart"
               @onNextLevel="onNextLevel"


    ></AppResult>
    <div v-else >404</div>
  </transition>
  </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      state: "start", 
      stats: {
          succes: 0,
          error: 0
      },

      message : {
        text : " " ,
        type : " "
      },
      questMax: 3,
      level: 0,
      levels: [
        {
          min: 10,
          max: 20,
          range: 5,
          variants: 2,
          time: 7
        },
        {
          min: 100,
          max: 200,
          range: 25,
          variants: 4,
          time: 6
        },
        {
          min: 300,
          max: 800,
          range: 50,
          variants: 6,
          time: 5
        },
        {
          min: 800,
          max: 1500,
          range: 80,
          variants: 6,
          time: 4
        },
        {
          min: 1000,
          max: 2200,
          range: 150,
          variants: 6,
          time: 3
        }
      ]
    }

  },
  computed: {
    questDone(){
      return this.stats.succes + this.stats.error;
    },

    progressStyles(){
      return {
         width: ((this.questDone / this.questMax) * 100) + "%"
      } 
    }
  },
  methods: {
     onStart(){
      this.state = 'quest';
      this.stats.succes = 0;
      this.stats.error = 0;
     },
     onNext(){
      if (this.questDone < this.questMax) {
        this.state = 'quest';
      } else{
        this.state = 'result';
      }
      
     },
     onNextLevel(){
       this.level++;
       this.stats.succes = 0;
       this.stats.error = 0;
       this.state = 'quest';
     },

      onSucces(){
        this.state = "msg";
        this.message.text = "Молодец!";
        this.message.type = "succes";
        this.stats.succes++;
      } ,

      onError(mes){
        this.state = "msg";
        this.message.text = mes;
        this.message.type = "error";
        this.stats.error++;
      },
      ontimeOut(mes){
        this.state = "msg";
        this.message.text = mes;
        this.message.type = "error";
        this.stats.error++;
      }
  }
}
</script>




<style scoped>
.traning {
  font-family: 'Open Sans', sans-serif;
  max-width: 700px;
  margin: 20px auto;
}

h1,
h2 {
  font-weight: normal;
  text-align: center;
}


.progressbar{
    width: 100%;
    height: 10px;
    margin: 10px auto;
    border: 1px solid #333;
    border-radius: 5px;
    overflow: hidden;
}


.progressbar__load-line{
   width: 0;
   height: 100%;
   background-color: #034777;
   transition: width .5s;

}


.flip-enter-active{
  animation: flipInX  .3s linear;

}

.flip-leave-active{
  animation: flipOutX .3s linear;

}

 @keyframes flipInX {
   from{
      transform: rotateX(90deg);
   }
   to{
     transform: rotateX(0deg);
   }
 }

  @keyframes flipOutX {
   from{
      transform: rotateX(0deg);
   }
   to{
     transform: rotateX(90deg);
   }
 }


</style>
