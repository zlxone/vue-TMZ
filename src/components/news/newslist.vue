<template>
  <div>
    <div id="newslist" class="tmzbody">
      <v-scroll :on-refresh="onRefresh" :on-infinite="onInfinite">
        <ul>
          <li v-for="news in newslist1">
            <div class="newsimg" @click="getednews(news,$event)">
              <a>
                <img :src="news.thumbnail_pic_s" lazy_src="news.thumbnail_pic_s">
              </a>
            </div>
            <div class="newsinfo" @click="getednews(news,$event)">
              <div class="newsinfoname">
                <p>{{news.title}}</p>
                <!--<a></a>-->
              </div>
              <div class="newsinfofoot">
                <div class="newsinfotime">{{news.date}}</div>
                <div class="newsinfomark"><span>10</span></div>
              </div>
            </div>
          </li>

          <li v-for="news in newslist2">
            <div class="newsimg" @click="getednews(news,$event)">
              <a>
                <img :src="news.thumbnail_pic_s" lazy_src="news.thumbnail_pic_s">
              </a>
            </div>
            <div class="newsinfo" @click="getednews(news,$event)">
              <div class="newsinfoname">
                <p>{{news.title}}</p>
                <!--<a></a>-->
              </div>
              <div class="newsinfofoot">
                <div class="newsinfotime">{{news.date}}</div>
                <div class="newsinfomark"><span>10</span></div>
              </div>
            </div>
          </li>
        </ul>
      </v-scroll>
    </div>
    <newsinfo :news="getnews" ref="news"></newsinfo>
  </div>

</template>

<script>
  import newsinfo from './newsinfo.vue'
  import refresh from './refresh.vue'

  export default {
    data () {
      return {
        getnews: {},
        tsrc: './assets/logo.png',
//                url: 'http://topTMZ.top:8080/tmz/yundisc/newslist.json',
        url0: 'http://topTMZ.top:8080/tmz/news/list',
        type:"top",
        counter: 1, //默认已经显示出10条数据 count等于一是让从16条开始加载
        num: 10,  // 一次显示多少条
        pageStart: 0, // 开始页数
        pageEnd: 0, // 结束页数
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
    watch: {
      title: function () {
        console.log("变化 " + this.title)
        this.type=this.title

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
        this.getnewlist(this.url0)
      }
    },
    mounted: function () {
//            var url='http://v.juhe.cn/toutiao/index?type=guoji&key=bfb89342daea5131b3d482820741da12';
//            var url='https://api.douban.com/v2/movie/top250?count=10';
//             var url='http://topTMZ.top:8080/tmz/yundisc/newsguoji.json';
      this.getnewlist(this.url0);

    },
    methods: {
      getnewlist(url){
        this.$http.post(url, {"type":this.type}, {emulateJSON: true})
          .then(
            (data) => {
              console.log(data.body.data.data.length+"  "+data);
              this.newslist1 = [];
              this.newslist1 = data.body.data.data.slice(0, 10);
            },
            (error) => {
              console.log(error);
            }
          );
      },
      getednews(news, event){
        this.getnews = news;
        this.$refs.news.show();
      },
      onRefresh(done) {
        this.getnewlist(this.url0);

        done() // call done

      },
      onInfinite(done) {
        let vm = this;
        this.$http.post(url, {"type":this.type}, {emulateJSON: true}).then((data) => {
          vm.counter++;
          vm.pageEnd = vm.num * vm.counter;
          vm.pageStart = vm.pageEnd - vm.num;
          let arr = data.body.data.data;
          let i = vm.pageStart;
          let end = vm.pageEnd;
          for (; i < end; i++) {
            let obj = {};
            obj = arr[i];
            vm.newslist2.push(obj);
            if ((i + 1) >= data.body.data.data.length) {
              this.$el.querySelector('.load-more').style.display = 'none';
              return;
            }
          }
          done() // call done
        }, (data) => {
          console.log('error');
        });
      }
    },
    components: {
      newsinfo,
      'v-scroll': refresh
    }

  }


</script>

<style>
  /*.tmzbody{*/
  /*position: absolute;*/
  /*top: 50px;*/
  /*left: 0;*/
  /*bottom: 50px;*/
  /*width: 100%;*/
  /*!*margin-bottom: 80px;*!*/
  /*z-index: 10;*/
  /*!*border: solid 3px black;*!*/
  /*overflow-y: scroll;*/
  /*padding:0 8px;*/
  /*}*/
  .tmzbody ul {
    display: block;
    text-align: left;
    width: 100%;
  }

  .tmzbody ul li {
    display: flex;
    float: left;
    height: 80px;
    /*border: solid 1px red;*/
    line-height: 80px;
    list-style-type: none;
    border-bottom: solid 1px gainsboro;
    /*background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='100%' height='1'><rect fill='#c8c7cc' x='0' y='0' width='100%' height='0.5'/></svg>");*/
    /*margin: 0 12px;*/
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
    font-size: 20px;
    line-height: 50px;
  }

  .newsinfoname p {
    height: 50px;
    width: auto;
    font-size: 18px;
    line-height: 23px;
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
