<template>
  <div class="main">
      <div class="title">About</div>
      <div class="info">
          <p>This project was made using VueJs without centralized storage or routing</p>
          <p>It is inspired in the pomodoro technique developed by Francesco Cirillo </p>
          <p>Source Code</p>    
      </div>
  </div>
</template>

<script>
export default {
    props:['show']
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
    p:nth-child(2){
        margin-top:2rem;
    }
    p:nth-child(3){
        margin-top:4rem;
        color:wheat;
    }
</style>