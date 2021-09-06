<template>  
  <div v-if="opens" class="sidebar">
    <div class="close" @click="$emit('closeMenu') ">
        X
    </div>
    <ul>
        <li @click="$emit('modal',1)" >Show All</li>
        <li @click="$emit('modal',2)"> Settings</li>
        <li @click="$emit('modal',3)">About</li>
    </ul>
  </div>
</template>

<script>
export default {
    props: ['opens'],
    openModal(){

    }
}
</script>

<style scoped>
    .sidebar{
        z-index:51;
        /* display:none; */
        height:100vh;
        position: fixed;
        width:100%;
        background-color:red;
        /* opacity:1; */
        color:white;
    }
    .close{
        position: absolute;
        top:1rem;
        font-size:3rem;
        right:0;
        padding-right:2rem;
        cursor:pointer;
    }
    ul{
        padding:0;
        margin: 0;
        display:flex;
        flex-direction: column;
        list-style: none;
        text-decoration: none;
        align-items: center;
        height:100%;
        justify-content: center;
    }
    li{
        margin-bottom:2rem;
        font-size: 2rem;
    }
</style>