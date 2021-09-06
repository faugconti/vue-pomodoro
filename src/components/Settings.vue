<template>
  <div class="main">
      <div class="title">Settings</div>
      <div class="timer">
          <div class="timer__title">Timer</div>
          <div class="timer__container">
              <button 
                @click="changeTime('HIGH')"
                :class="{active : timerMode ==='HIGH'}">30</button>
              <button 
                @click="changeTime('MID')"
                :class="{active : timerMode ==='MID'}">25</button>
              <button 
                @click="changeTime('LOW')"
                :class="{active : timerMode ==='LOW'}">10</button>
          </div>
      </div>
      <div class="break">
          <div class="timer__title">Break</div>
          <div class="break__container">
              <button 
                :class="{active : breakMode ==='HIGH'}"
                @click="changeBreak('HIGH')">20</button>
              <button 
                :class="{active : breakMode ==='MID'}"
                @click="changeBreak('MID')">10</button>
              <button 
                :class="{active : breakMode ==='LOW'}"
                @click="changeBreak('LOW')">5</button>
          </div>
      </div>
      <div class="sound">
          <div class="timer__title">Sound</div>
          <div class="sound__container" @click="toggleSound">
            <img 
            v-if="soundActivated"
            src="../assets/bellActive.svg"  alt="bell"> 
            <img 
            v-else
            src="../assets/bell.svg"  alt="bell"> 
          </div>
      </div>
      
      
  </div>
</template>

<script>
export default {
    props: {
        timer:{
            type: Object,
            required:true
        },
        brek: {
            type: Object,
            required: true
        },
        sound: {
            type:Object,
            required: true
        },
        
    },
    data(){
        return{
            
        }
    },
    computed:{
        soundActivated(){
            return this.sound.value;
        },
        soundHandler(){
            return this.sound.changeSound;
        },
        timerMode(){
            return this.timer.currentTimer;
        },
        changeTime(){
            return this.timer.changeTimer;
        },
        breakMode(){
            return this.brek.currentBreak;
        },
        changeBreak(){
            return this.brek.changeBreak;
        }
    },
    methods:{
        basic(){
            console.log(this.timerMode);
        },
        toggleSound(){
            console.log('toggle sound')
            this.soundHandler();
        }
    }
}
</script>

<style scoped>
    button{
        color:red;
        width:5rem;
        background:white;
        border-radius:1rem;
        height:3rem;
        margin: 0 0.5rem;
        font-size: 1rem;
        border:solid white 2px;
        font-weight: bold;
    }
    .active{
        background:red;
        color:white;
    }
    .title{
        font-size:2rem;
        /* float:left; */
        margin-top:1rem;
        text-align: left;
        margin-left:2rem;
    }
    .timer__title{
        text-align: left;
        /* color:red; */
        margin-left:2rem;
        text-decoration: underline;
    }
    .timer__container{
        display:flex;
        justify-content: center;
        align-items: center;
        margin-top:1rem;
    }

    .sound__container{
        text-align: center;
        width:100%;
        height:10%;        fill: blue;

    }
    img{
        margin: 0 auto;
        display:block;
        max-width: 25%;
        /* background:  red; */
        fill: blue;
    }
    @media(min-width:1000px){
        .sound__container{
        text-align: center;
        width:100%;
        height:5%;       
    }
        img{
            max-width: 10%;
        }
    }
</style>