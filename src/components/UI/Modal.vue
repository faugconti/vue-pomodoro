<template>
        <div class="backdrop">
            <div class="super"></div>
            <div class="close" 
                @click="$emit('closeMenu')">X</div>
            <About v-if="type===3" />
            <Settings  
                :sound = "sound"
                :timer = "timer" 
                :brek = "breaks"
                v-if="type===2" />
            <Log :log="log" v-if="type===1" />
            <!-- {{timer ? 'si' : 'no'}} -->
        </div>
</template>

<script>
import About from '../../components/About';
import Settings from '../../components/Settings';
import Log from '../../components/Log';

export default {
    props: {
        'log':{
            type:Object
        },
        'type': {
            required:false,
            type:Number
        },
        'sound': {
            required:true,
            type: Object,
        },
        'timer' : {
            required: true,
            type: Object
        },
        'breaks' : {
            required : true,
            type : Object
        }
    },
    components: {
        About,
        Settings,
        Log
    }
}
</script>

<style scoped>
    .hide{
        display:none;
    }
    .backdrop{
        /* display:block; */
        position:fixed;
        background:darkred;
        height:80vh;
        width:90%;
        margin:10vh 5%;
        border-radius: 1rem;
        z-index:55;
        opacity:0.95;
        border: 2px solid white;
        font-family: 'Rock Salt';
        color:white;
        overflow: scroll;
        /* overflow-y:hidden; */

    }
    .close{
        font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
        color:white;
        font-size: 2rem;
        margin-top:1rem;
        margin-right:2rem;
        float:right;
        cursor:pointer;
    }
    @media(min-width:1000px){
        .super{
            background:black;
            height:100vh;
            position:fixed;
            z-index:50;
        }
        .backdrop{
            height:40%;
            width:30%;
            overflow:auto;
            margin: 50vh 35%;
        }
        ::-webkit-scrollbar { 
        display: none; 
        }
    }

</style>