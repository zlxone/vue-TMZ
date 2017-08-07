<template>
    <div class="back" @click="backlist">
        <img src="../../assets/back.png">
    </div>
</template>

<script>
    export default {
        data () {
            return {}
        },
        created (){
        },
        methods: {
            back(){
                this.showflag=false;
            }
        },
        components: {}
    }
</script>

<style>
    .back{
        position: fixed;
        margin-left: -200px;
        margin-top: 50%;
        display: inline-block;
        background: rgba(0,0,0,0.5);
        border-radius: 50%;
        text-align: center;
        /*z-index: 90;*/
        width: 50px;
        height: 50px;
    }
    .back img{
        margin-right: 10px;
        margin-top: 10px;
        width: 30px;
        height: 30px;
    }
</style>