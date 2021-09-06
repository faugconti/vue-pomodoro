<template>
  <div class="main"> 
      <div class="counter">
            <p> {{counter}} </p> 
      </div>
      <div class="container">
          <buttonCmp :clicked="startTimer" type="normal">Start</buttonCmp>
          <buttonCmp :clicked="stopTimer" type="normal">Stop</buttonCmp>
          <buttonCmp :clicked="resetTimer" type="normal">Reset</buttonCmp>
          <buttonCmp :clicked="breakTimer" type="break">Relax</buttonCmp>
      </div>
    <audio v-if="doSound && soundIsOn" controls id="myVideo" autoplay loop hidden>
        <source src="../assets/sound.wav" type="audio/wav">
         Your browser does not support the audio element.
    </audio>
      
    </div>
</template>

<script>
import Button from './UI/Button';
export default {
    components: {
        buttonCmp: Button,
    },
    props:['timerMode','sound','logHandler','relax'],
    data(){
        return { 
            breakMode: false,
            soundIsOn: false,
            timerOn: false,
            completed:false,
            currentCount: {
                minutes: 0,
                seconds: 2
            },
            timerfunc: null,
        }
    },
    computed:{
       doBreak(){
           return this.relax.breakIsOn;
       },
       doSound(){
           return this.sound
       },
       counter: function(){
           const seconds = this.currentCount.seconds <10 ? '0'+this.currentCount.seconds : this.currentCount.seconds;
           const minutes = this.currentCount.minutes <10 ? '0'+this.currentCount.minutes : this.currentCount.minutes;
           return minutes+':'+seconds
       }
    },
    watch: {
        doBreak(){
            console.log('activated')
        },
        timerMode: function(mode){
            console.log('new mode ',mode);
            if(!this.timerOn){
                this.setTimer();
            }
        }
    },
    methods:{
        makeSound(){
            this.soundIsOn = true;
            setTimeout(()=>{
                this.soundIsOn=false; 
            },5750);
        },
        breakTimer(){
            console.log('break timer activated');
            this.$emit('relax');
        },
        setBreak(){
            this.completed=false;
            if(this.relax==='HIGH'){
                this.currentCount = {
                    minutes: 20,
                    seconds: 0
                }
            }
            else if(this.timerMode==='MID'){
                this.currentCount = {
                    minutes: 10,
                    seconds: 0
                }
            }else{
                this.currentCount = {
                    minutes: 5,
                    seconds: 0
                }
            }
        },
        setTimer(){
            this.completed= false;
            if(this.timerMode==='HIGH'){
                this.currentCount = {
                    minutes: 30,
                    seconds: 0
                }
            }
            else if(this.timerMode==='MID'){
                this.currentCount = {
                    minutes: 25,
                    seconds: 0
                }
            }else{
                this.currentCount = {
                    minutes: 10,
                    seconds: 0
                }
            }
        },
        startTimer(){
            console.log('start pressed');

            if(this.timerOn){
                console.log('already running');
                return
            }
            else if(this.completed){
                return
            }

            this.timerOn=true;
            this.timerfunc = setInterval(()=>{
                console.log('tic')
                if (this.currentCount.seconds==0){
                    if(this.currentCount.minutes==0){
                        console.log('end');
                        this.makeSound();
                        this.stopTimer();
                        this.completed = true;
                        console.log(this.logHandler);
                        this.logHandler.timers();
                    }
                    else{
                        this.currentCount.minutes--;
                        this.currentCount.seconds=59;
                    }
                }
                else{
                    if(this.currentCount.minutes==0 && 
                        this.currentCount.seconds==0){
                        
                            console.log('hola')
                            this.clearTimer();
                    }
                    else
                        this.currentCount.seconds--;
                }
            },1000);
        },
        clearTimer(){
            console.log('inside clear')
            window.clearInterval(this.timerfunc);
        },
        stopTimer(){
            this.timerOn=false;
            window.clearInterval(this.timerfunc);
            console.log('stopping timer');
            console.log('timer',this.timerOn);
        },
        resetTimer(){
            if(this.timerOn){
                this.stopTimer();
                
            }
            this.completed = false;
            console.log('inside reset');
            console.log(this.timerMode);
            this.setTimer();
        },
    },
    beforeUpdate(){
        console.log('props or state changed')
    }
}
</script>

<style scoped>
    .main{
        height:100%;
    }
    .counter{
        text-align: center;
        /* padding-top:2rem; */
        color:white;
        font-size: 5rem;
        height:30%;
        /* background:black; */
        display:flex;
        align-items: center;
        justify-content: center;
    }
    .counter p{
        margin:0;
    }
    .container{
        /* max-height: 70vh; */
        min-height: 50%;
        /* margin-top:1rem; */
        /* height:10%; */
        display:flex;
        flex-direction: column;
        flex-wrap: wrap;
        align-items: center;
        z-index:-1;
    }

    @media(min-width:1000px){
        .main{
            height:100%;
            
        }
        .counter{
            margin: auto 0;
        }
      .container{
          flex-direction: row;
          justify-content: center;
          align-items: flex-start;
          grid-column-start: 0;
          grid-column-end:1;
          /* flex-wrap: wrap; */
          /* height: 100%; */
          
      }
      
}
</style>