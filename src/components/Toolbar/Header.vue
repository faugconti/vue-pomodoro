<template>
  <div class="Header" >
    <div class="Header__Logo">TomatoTimer</div>
    <div @click="openMenu" class="Header__menu">Click</div>
  </div>
</template>

<script>
export default {
    methods:{
        openMenu(){
            this.$emit('openMenu')
        }
    }
}
</script>

<style scoped>
    .Header{
        z-index:50;
        background: rgb(216,31,31);
        background: linear-gradient(180deg, rgba(216,31,31,1) 0%, rgba(168,34,40,1) 100%);
        height:4rem;
        color:white;
        display:flex;
        align-items: center;
        justify-content: space-between;
        position:fixed;
        width:100%;
        font-family: 'Shadows Into Light';
    }
    .Header__Logo{
        padding-left: 2rem;
        font-size: 1.5rem;
    }

    .Header__menu{
        margin-right:2rem;
    }
    

    @media(min-width:1000px){
        .Header{
            font-family: 'Shadows Into Light';
            height:6rem;
            background: linear-gradient(180deg, rgba(216,31,31,1) 0%, rgba(168,34,40,0.04) 80%);
        }
        .Header__Logo{
            padding-left: 6rem;
            font-size: 3rem;
        }
    }
</style>