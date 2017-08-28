<template>
  <div>
    <div id="newslist2" class="tmzbody">
      <mt-loadmore :top-method="loadTop" :bottom-method="loadBottom" :bottom-all-loaded="allLoaded"
                   :topPullText="topPullText" :topDropText="topDropText" :topLoadingText="topLoadingText"
                   :bottomDropText="bottomDropText" :bottomLoadingText="bottomLoadingText"
                   :bottomPullText="bottomPullText" :auto-fill="false" ref="loadmore">
        <ul>
          <li v-for="news in newslist1">
            <div class="newsimg" @click="getednews(news,$event)">
              <a>
                <img :src="news.thumbnailPicS" lazy_src="news.thumbnailPicS">
              </a>
            </div>
            <div class="newsinfo" @click="getednews(news,$event)">
              <div class="newsinfoname">
                <p>{{news.title}}</p>
                <!--<a></a>-->
              </div>
              <div class="newsinfofoot">
                <div class="newsinfotime">{{news.date | formatDate}}</div>
                <div class="newsinfomark"><span>50</span></div>
              </div>
            </div>
          </li>
        </ul>

      </mt-loadmore>
    </div>
    <newsinfo :news="getnews" ref="news"></newsinfo>

  </div>

</template>

<script>
  import newsinfo from './newsinfo.vue'
  import {formatDate} from '../../assets/js/formatDate'
  import {Indicator, Loadmore} from 'mint-ui'

  export default {
    data () {
      return {
        getnews: {},
        tsrc: './assets/logo.png',
        url0: 'http://topTMZ.top:8080/tmz/news/list',
        type: "top",
        topStatus: '',
        pnum0: 0,
        psum0: 10,
        topPullText: '下拉刷新',
        topDropText: '释放更新',
        topLoadingText: '加载中...',
        bottomPullText: '上拉刷新',
        bottomDropText: '释放更新',
        bottomLoadingText: '加载中...',
        allLoaded: false,
        scrollMode: "auto", //移动端弹性滚动效果，touch为弹性滚动，auto是非弹性滚动
        newslist1: [],
        newslist2: [],//下拉列表
        newslist: [
          {
            "uniquekey": "ffb134f252e35a556795d7dcd7c65bd9",
            "title": "多图｜新疆某边境多兵种联合演练 “六位一体”歼灭暴恐分子",
            "date": "2017-07-26 15:58",
            "category": "头条",
            "author_name": "@央广军事",
            "url": "http://mini.eastday.com/mobile/170726155824378.html",
            "thumbnail_pic_s": "http://04.imgmini.eastday.com/mobile/20170726/20170726155824_eb1496e524f39ab3323259d9e2521bd1_4_mwpm_03200403.jpg",
            "thumbnail_pic_s02": "http://04.imgmini.eastday.com/mobile/20170726/20170726155824_eb1496e524f39ab3323259d9e2521bd1_2_mwpm_03200403.jpg",
            "thumbnail_pic_s03": "http://04.imgmini.eastday.com/mobile/20170726/20170726155824_eb1496e524f39ab3323259d9e2521bd1_1_mwpm_03200403.jpg"
          },
          {
            "uniquekey": "0485468186c3ee493471a6e279c490db",
            "title": "日本多地持续高温 造成6人死亡6千余人入院",
            "date": "2017-07-26 16:06",
            "category": "头条",
            "author_name": "环球网",
            "url": "http://mini.eastday.com/mobile/170726160659694.html",
            "thumbnail_pic_s": "http://01.imgmini.eastday.com/mobile/20170726/20170726160659_e3776b7ec6fa4b4d6ece2baff49f6a22_1_mwpm_03200403.jpg"
          },
          {
            "uniquekey": "c5300e4bcd51c73e5945569caadaf07c",
            "title": "美国最先进侦察机：飞行员要穿宇航服，被中国打下来五架",
            "date": "2017-07-26 15:28",
            "category": "头条",
            "author_name": "123军情观察室",
            "url": "http://mini.eastday.com/mobile/170726152838882.html",
            "thumbnail_pic_s": "http://08.imgmini.eastday.com/mobile/20170726/20170726_e58e84155bf088891a89ad448d542243_cover_mwpm_03200403.jpeg",
            "thumbnail_pic_s02": "http://08.imgmini.eastday.com/mobile/20170726/20170726_6826c8f55df9d1065a764f4c8382466b_cover_mwpm_03200403.jpeg",
            "thumbnail_pic_s03": "http://08.imgmini.eastday.com/mobile/20170726/20170726_2f2fd67a7d6e2e4b03ee0e8c399f4b4b_cover_mwpm_03200403.jpeg"
          }
        ]
      }
    },
    props: ['title'],
    filters: {
      formatDate(time) {
        var date = new Date(time);
        return formatDate(date, 'yyyy-MM-dd hh:mm');
      }
    },
    watch: {
      title: function () {
        console.log("变化 " + this.title)
        this.type = this.title

        /*        this.url0 = 'http://topTMZ.top:8080/tmz/yundisc/';

         if (this.title === 'guoji') {
         this.url0 = this.url0 + 'newsguoji.json'
         }
         if (this.title === 'top') {
         this.url0 = this.url0 + 'newslist.json'
         }
         if (this.title === 'shehui') {
         this.url0 = this.url0 + 'newsshehui.json'
         }
         if (this.title === 'guonei') {
         this.url0 = this.url0 + 'newsguonei.json'
         } */

        console.log("url0  " + this.url0)
        this.init(this.url0)
      }
    },
    mounted: function () {
      this.init(this.url0);
    },
    methods: {
      init: function (url) {
        this.newslist1 = [];
        this.pnum0 = 0;
        Indicator.open();
        setTimeout(() => {
          this.getnewslist(url, 0);
          Indicator.close();
        }, 500);
      },
      getnewslist: function (url, pnum) {
        this.$http.post(url, {"type": this.type, "pnum": pnum, "psum": this.psum0}, {emulateJSON: true})
          .then(
            (data) => {
              console.log(data);
              if (data.body.code === 0) {
                this.newslist2 = data.body.data;
                this.newslist1 = this.newslist1.concat(this.newslist2);
              } else {
//                this.allLoaded = true;// 若数据已全部获取完毕
                console.log("no data");
              }

            },
            (error) => {
              console.log(error);
            }
          );
      },
      getednews: function (news, event) {
        this.getnews = news;
        this.$refs.news.show();
      },
      loadTop: function () {         //下拉加载
        console.log(this.pnum0);
        this.init(this.url0);
        this.$refs.loadmore.onTopLoaded();// 固定方法，查询完要调用一次，用于重新定位
      },
      loadBottom: function () {// 上拉加载
        this.pnum0 += this.psum0;
        setTimeout(() => {
          this.getnewslist(this.url0, this.pnum0);
        }, 300);
        this.$refs.loadmore.onBottomLoaded();// 固定方法，查询完要调用一次，用于重新定位
      }
    },
    components: {
      newsinfo,
      'mt-loadmore': Loadmore
    }

  }


</script>

<style>


  .mint-loadmore-text {
    color: gray;
    font-size: 16px;
    font-family: "Microsoft Himalaya";
  }

  .tmzbody ul {
    display: block;
    text-align: left;
    width: 100%;
  }

  .tmzbody ul li {
    display: flex;
    float: left;
    border-bottom: solid 1px gainsboro;
    width: 100%;
  }

  .newsimg {
    display: block;
    flex: 0 0 80px;
    float: left;
    /*border: solid 1px blue;*/
    height: 70px;
    width: 80px;
    margin: 5px;
    text-align: left;
  }

  .newsimg a img {
    height: 70px;
    width: 80px;
  }

  .newsinfo {
    flex: 1;
    float: left;
    /*border: solid 1px yellow;*/
    height: 70px;
    width: 100px;
    margin: 5px;
    display: block;
  }

  .newsinfoname {
    /*border: solid 1px black;*/
    height: 50px;
    /*width: 100%;*/
    /*font-size: 20px;*/
    line-height: 50px;
  }

  .newsinfoname p {
    height: 50px;
    width: auto;
    font-size: 18px;
    line-height: 25px;
    color: black;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
  }

  .newsinfofoot {
    /*border: solid 1px black;*/
    height: 16px;
    margin-top: 3px;
  }

  .newsinfotime {
    float: right;
    /*border: solid 1px blue;*/
    height: 16px;
    width: auto;
    /*margin: 5px 0;*/
    font-size: 12px;
    color: #757575;
    line-height: 16px;
    text-align: left;
    /*padding-left: 10px;*/
  }

  .newsinfomark span {
    float: left;
    /*border: solid 1px blue;*/
    height: 16px;
    width: auto;
    /*margin: 5px 0;*/
    font-size: 12px;
    color: #757575;
    line-height: 16px;
    text-align: right;
    /*padding-right: 10px;*/
  }
</style>
