<template>
  <button @click="clicked" :class="type">
      <slot></slot>
  </button>
</template>

<script>
export default {
    props: {
        'type':String,
        'clicked': {
            required:false,
            type:Function,
            default: ()=>{}
        },
    }
}
</script>

<style scoped>
    button{
        max-height:4rem;
        min-height: 2rem;
        width:15rem;
        margin: 0.75rem;
        color:white;
        font-size: 2rem;
        text-decoration: none;
        outline: none !important;
        z-index:2;
    }
    .normal{
        background:#cf2222;
        border:3px solid #FF0000;
        border-radius: 25px;
    }
    .normal:hover{
        background:darkred;
    }
    .normal:active{
        background:white;
        color:Red;
    }
    .break{
        color:red;
        background:white;
        border-radius: 25px;
        border:3px solid #FF0000;
    }
    .break:hover{
        background:darkred;
        color:white;
    }
    .break:active{
        background:red;
        color:white;
    }
    
</style>