<template>
  <div class="main">
    <div class="title">Log</div>
    <div class="counter">
      <div  class="empty" >{{log.timers}} pomodoros completed</div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['log']
}
</script>

<style scoped>

  .main{

  }
  .title{
      font-size:2rem;
      /* float:left; */
      margin-top:1rem;
      text-align: left;
      margin-left:2rem;
    }
  .counter{
    margin-top:2rem;
    font-size:1.6rem;
  }
  .empty{
    margin-top:1rem;
  }
  
</style>