<template>
  <div id="app">
    <app-header @openMenu='clicked'></app-header>
    <modal 
      :log="log"
      :sound="soundObj"
      :timer="timerObj"
      :breaks="breakObj"
      :type="currentModal" 
      v-show="modalOpen" 
      @closeMenu="closed">
       
    </modal>  
    <sidebar 
      @modal="openModal($event)" 
      @closeMenu='closed' 
      :opens="menuOpen" />

    <div class="wrapper">
      <Timer
        @relax="breakActivated=true"
        :relax="relaxObj"
        :logHandler="logObj" 
        :sound="sound"
        :breakMode="breakMode"
        :timerMode="timerMode"></Timer>
    </div>
    <div class="tomato">
      
      <!-- <img src="./asssets/tomato.png" alt=""> -->
    </div> 
  </div>
</template>

<script>
import Header from './components/Toolbar/Header';
import Timer from './components/Timer'
import Sidebar from './components/Toolbar/Sidebar';
import Modal from './components/UI/Modal';
export default {
  
  components: {
    'appHeader': Header,
    'Timer':Timer,
    'sidebar': Sidebar,
    'modal': Modal,
  },
  data(){
    return{
      breakActivated:false,
      menuOpen: false,
      modes: ['LOW','MID','HIGH'],
      timerMode: 'MID',
      breakMode: 'MID',
      modalOpen: false,
      currentModal: null,
      sound: true,
      log: {
        timers: 0,
        breaks:0
      }
      
    }
  },
  computed:{
    relaxObj(){
      return {
        breakIsOn: this.breakActivated,
        breakMode: this.breakMode
      }
    },
    logObj(){
      return {
        timers: this.updateCount.bind(this,'timer'),
        breaks: this.updateCount.bind(this,'break')
      }
    },
    soundObj(){
      return{
        value: this.sound,
        changeSound: this.soundHandler
      }
    },
    timerObj(){return {
      currentTimer : this.timerMode,
      changeTimer : this.changeTimeHandler
    }},
    breakObj(){
      return {
        currentBreak: this.breakMode,
        changeBreak : this.changeBreakHandler
      }
    }
  },
  methods: {
    updateCount(type){
      if(type==='timer'){
        this.log.timers++;
      }else{
        this.log.breaks++;
      }
    },
    soundHandler(){
      this.sound = !this.sound;
    },
    changeBreakHandler(type){
      console.log(type)
      if(this.breakMode === type) 
        return
      console.log('changing break timer');
      this.breakMode = type;
    },
    changeTimeHandler(type){
      console.log(type)
      if(this.timerMode === type) 
        return
      console.log('changing timer');
      this.timerMode = type;
    },
    openModal(menuType){
      console.log(menuType);
      this.modalOpen = true;
      this.menuOpen = false;
      this.currentModal = +menuType;
    },
    closed(){
      this.menuOpen= false;
      this.modalOpen = false;
      this.currentModal = null;
    },
    clicked(){
      console.log('open')
      this.menuOpen=! this.menuOpen;
      this.modalOpen = false;
      console.log(this.menuOpen)
    }
  }


}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height:100%;
  

  background: rgb(216,31,31);
  background: linear-gradient(180deg, rgba(216,31,31,1) 0%, rgba(97,11,15,1) 100%);
  }

html{
  height:100%;
}
body{
  /* overflow: none; */
  margin:0;
  height:100%;
  /* overflow-y:hidden;
  overflow-x: hidden;  */
}
.wrapper{
  box-sizing: border-box;
  padding-top:4rem;
  height:100%;
  /* background:green; */
  /* background:black; */
}

.tomato{
  /* float:right; */
  opacity: 0.2;
  background-image: url('./assets/tomato.png');
  background-repeat: no-repeat;
  height: 20rem;
  width:100%;
  /* background:black; */
  position:absolute;
  bottom:0;
  right:0;
  
}

@media(min-width:1000px){
      .tomato{
        width:50%;
      }
}
</style>
