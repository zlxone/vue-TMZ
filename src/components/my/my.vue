<template>
    <div id="my">
        <div class="tmzhead">
            <div class="tmzheadtitle">
                <p>我的</p>
            </div>
        </div>
        <div class="tmzbody">
            <div class="myinfo">
                <div class="myimg">
                    <a><img src="../../assets/logo.png"></a>
                </div>
                <div class="myinfos">
                    <p class="myname">千夫长<span>male</span></p>
                    <p class="mymark">南园春半踏青时，风和闻马嘶。青梅如豆柳如眉，日长蝴蝶飞。
                      花露重，草烟低，人家帘幕垂。秋千慵困解罗衣，画堂双燕归。</p>
                </div>
            </div>
          <div class="mynote">
            <textarea></textarea>
          </div>
            <div class="mylist">
                <ul>
                    <li><a>我的收藏</a></li>
                    <li><a>我的收藏</a></li>
                    <li><a>我的收藏</a></li>
                    <li><a>我的收藏</a></li>
                    <li><a>设置</a></li>
                </ul>
            </div>
        </div>

<div id="content">
</div>

    </div>
</template>

<script>

    export default {
        data () {
            return {
                msg: 'my'
            }
        },
        methods: {
        },
        components: {}
    }
</script>

<style>
    .myinfo{
      color: black;
      display: flex;
        /*border: solid 1px red;*/
        height: 120px;
        width: 100%;
        text-align: center;
      padding: 8px;
      border-bottom: solid 1px grey;
    }
    .myinfo div{
      float: left;
      text-align: center;
    }
    .myimg{
      flex: 0 0 100px;
      height: 100px;
      border: solid 1px grey;
    }
    .myimg a img{
      width: 100px;
      height: 100px;
    }
    .myinfos{
      flex: 1;
      margin-left: 4px;
    }
    .myname{
      /*border: solid 1px black;*/
      width: 100%;
      height: 26px;
      color: black;
      font-size: 22px;
      line-height: 26px;
      text-align: left;
    }
    .mymark{
      margin-top: 4px;
      /*border: solid 1px black;*/
      width: 100%;
      height: 70px;
      line-height: 18px;
      color: black;
      font-size: 16px;
      text-align: left;
      /*text-overflow: ellipsis;*/
      overflow: auto;
      /*white-space: nowrap;*/
    }

    .mynote{
      height: 110px;
      border: solid 1px red;
    }
    textarea{
      height: 100%;
      width: 100%;
      font-size: 16px;
      color: black;
    }
    .mylist{
        border-top:solid 1px black ;
      text-align: center;
    }
    .mylist,ul,li,a{
        color: black;
        text-align: center;
        list-style-type: none;
    }
    .mylist ul li a{
      text-align: right;
    }

    /*.mylist ul li a:link{ color:white;}*/
    /*.mylist ul li a:hover{ color:white;font-weight: bolder;}*/
    /*.mylist ul li a:active{ color:white;font-weight: bolder;}*/
    /*.mylist ul li a:visited{ color:white;}*/
</style>
