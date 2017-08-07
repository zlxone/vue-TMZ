<template>
    <div id="logo">
        <div class="tmzlogo">
            <div class="logoimg">
                <img src="../../assets/userI.png" @click="toggle(true)">
            </div>
        </div>

        <!--<mu-raised-button label="undocked drawer" @click="toggle(true)"/>-->
        <mu-drawer :open="open" :docked="docked" @close="toggle()">
            <div class="userinfo">
                <div class="userimg">
                    <img src="../../assets/logo.png">
                </div>
                <div class="username">
                    <span>千夫长</span>
                </div>
                <div class="usermark">
                    <span>三等奖佛教东方魔第三方</span>
                </div>
                <div class="userart">
                    <ul>
                        <li><a>10</a></li>
                        <li>|</li>
                        <li><a>9</a></li>
                        <li>|</li>
                        <li><a>21</a></li>
                    </ul>
                </div>
            </div>
            <mu-list @itemClick="docked ? '' : toggle()">
                <mu-list-item><span class="drawerc">我的收藏</span></mu-list-item>
                <mu-list-item><span class="drawerc">我的收藏</span></mu-list-item>
                <mu-list-item><span class="drawerc">我的收藏</span></mu-list-item>
                <mu-list-item><span class="drawerc">我的收藏</span></mu-list-item>
                <mu-list-item><span class="drawerc">我的收藏</span></mu-list-item>

                <mu-list-item v-if="docked" @click.native="open = false" title="Close"/>
            </mu-list>
            <div class="sys">
                <span>反馈</span>
                <span>设置</span>
            </div>
        </mu-drawer>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                tlogo: './assets/userI.png',
                open: false,
                docked: true
            }
        },
        methods:{
            getleft(){
                console.log("LOGO");
            },
            toggle (flag) {
                this.open = !this.open
                this.docked = !flag
            }
        }
    }
</script>

<style>
    .tmzlogo{
        position: fixed;
        top: 0;
        left: 0;
        width: 53px;
        height: 56px;
        background-color: #7e57c2;
        border-radius:0 0 30px;
        z-index: 60;
    }
    .logoimg{
        width: 50px;
        height: 50px;
        /*background-color: powderblue;*/
        border-radius: 50%;
        text-align: center;
    }
    .logoimg img{
        width: 50px;
        height: 50px;
        border-radius: 50%;
        background-color: #7e57c2;
        margin-top: 5px;
        -moz-box-shadow: -1px -2px 8px  #000;
        -webkit-box-shadow: -1px -2px 8px  #000;
        box-shadow: -1px -2px 8px  #000;
    }
    .mu-drawer {
        width: 200px;
    }

    .drawerc {
        color: black;
    }

    .userinfo {
        color: black;
        width: 100%;
        height: 250px;
        border-bottom: solid 1px gainsboro;
    }

    .userimg{
        display: block;
        position: absolute;
        width: 80px;
        height: 80px;
        margin-left: 60px;
        margin-top: 80px;
    }
    .userimg img{
        width: 80px;
        height: 80px;
        border-radius: 50%;
        border: solid 2px grey;
    }
.username{
    width: 100px;
    height: 20px;
    position: absolute;
    top: 165px;
    left: 45px;
}
.username span{
    width: 100px;
    height: 20px;
    color: black;
    line-height: 20px;
    font-size: 18px;
    text-align: center;

}
    .usermark{
        width: 140px;
        height: 14px;
        position: absolute;
        top: 192px;
        left: 30px;
    }
    .usermark span{
        width: 140px;
        height: 12px;
        line-height: 12px;
        text-align: left;
        display: inline-block;
        color: grey;
        font-size: 12px;
        overflow: hidden;
        text-overflow: ellipsis;
    }
    .userart{
        position: absolute;
        top: 210px;
        left: 30px;
    }
    ul{
        display: inline-block;
        list-style-type: none;
    }
    .userart ul li{
        float: left;
        color: black;
        margin: 8px;
    }

.sys{
    width: 100%;
    border-top:solid 1px gainsboro;
    display: flex;
    position: absolute;
    bottom: 40px;
    padding-top: 10px;
    /*right: 50px;*/
}
    .sys span{
        flex: 1;
        color: black;
        /*margin-right: -70px;*/
        /*padding: 60px;*/
    }
</style>
