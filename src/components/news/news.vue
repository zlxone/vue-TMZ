<template>
    <div>
        <div  class="tmzhead">
            <div class="logo"></div>
            <div class="tmzheadtitle">
                <ul>
                    <li v-for="item in newsitems">
                        <!--<router-link to="/newslist">-->
                        <a @click="getnewslist(item.val)">{{item.name}}</a> |
                        <!--</router-link>-->
                    </li>
                </ul>
            </div>
            <div class="blank"></div>
        </div>

        <div class="newlists">
            <!--<router-view class="view"></router-view>-->
            <newslist :title="ptitle"></newslist>
        </div>




    </div>
</template>

<script>
    import newslist from './newslist2.vue'


    export default {
        data () {
            return {
                msg: 'my',
                ptitle: 'top',
                newsitems: [
                    {'name': '头条', 'val': 'top'},
                    {'name': '社会', 'val': 'shehui'},
                    {'name': '国内', 'val': 'guonei'},
                    {'name': '国际', 'val': 'guoji'},
                    {'name': '娱乐', 'val': 'yule'},
                    {'name': '体育', 'val': 'tiyu'},
                    {'name': '军事', 'val': 'junshi'},
                    {'name': '科技', 'val': 'keji'},
                    {'name': '财经', 'val': 'caijing'},
                    {'name': '时尚', 'val': 'shishang'}
                ]
            }
        },
        methods: {
            getnewslist(val){
                this.ptitle = val;
                console.log("list " + val + this.title);
            }
        },
        components: {newslist}
//        components:{
//            "test":{
//                props:["title"],
//                template:"<div>{{title}}</div>"
//            }
//        }
    }


</script>

<style>

/*.tmzhead{*/
    /*position: fixed;*/
    /*top: 0;*/
    /*left: 0;*/
    /*width: 100%;*/
    /*height: 50px;*/
    /*background-color: #7e57c2;*/
    /*text-align: left;*/
    /*z-index: 20;*/
/*}*/
/*.tmzheadtitle{*/
    /*width: auto;*/
    /*margin-top: 12px;*/
    /*margin-right: 50px;*/
    /*height: 34px;*/
    /*!*overflow: scroll;*!*/
    /*float: left;*/
/*}*/

.tmzheadtitle ul{
  -webkit-overflow-scrolling:touch;
    list-style-type: none;
    display:-webkit-box;
    display:-webkit-flex;
    display:-ms-flexbox;
    display:flex;
    -webkit-flex-wrap:nowrap;
    -ms-flex-wrap:nowrap;
    flex-wrap:nowrap;
    -webkit-box-pack:justify;
    -webkit-justify-content:space-between;
    -ms-flex-pack:justify;
    justify-content:space-between;
    /*background:#FF4878;*/
    padding:0;
    overflow:auto;
}
.tmzheadtitle ul li{
  /*border-left: 1px white solid;*/
  padding-left: 12px;
    -webkit-box-flex:1;
    -webkit-flex:1 0 auto;
    -ms-flex:1 0 auto;
    flex:1 0 auto;
    height: 34px;
    line-height: 34px;
    font-size: 18px;
    float: left;
    color: white;
    margin: 0 4px;
}

/*定义滚动条高宽及背景 高宽分别对应横竖滚动条的尺寸*/
::-webkit-scrollbar {
  display: none;
    /*width: 0px;*/
    /*height: 0px;*/
    /*background-color: rgba(0, 0, 0, 0.2);*/
}

.tmzheadtitle ul li a {
    text-decoration: none;
    color: white;
}

.tmzheadtitle ul li a:link {
    color: white;
}

.tmzheadtitle ul li a:hover {
    color: white;
    font-weight: bolder;
}

.tmzheadtitle ul li a:active {
    color: white;
    font-weight: bolder;
}

.tmzheadtitle ul li a:visited {
    color: white;
}

    .newlists{
        width: 100%;
    }
</style>
