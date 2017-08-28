<template>
  <div id="weather">

    <div class="tmzbody1">
      <div class="now">
        <div class="addr">
          {{weatherinfo1.city}}
        </div>
        <div class="winfo">
          {{weatherinfo1.weather}}
        </div>
        <div class="temp">
          {{weatherinfo1.temp}}<span>℃</span>
        </div>
        <div class="nowinfo">
          <div class="week">
            {{weatherinfo1.week}} 今天
          </div>
          <div class="t1t2">
            {{weatherinfo1.temphigh}} {{weatherinfo1.templow}}
          </div>
        </div>
      </div>
      <div class="todayinfo">
        <ul>
          <li v-for="tinfo in weatherinfo1.hourly">
            <div class="tinfo">
              <div>{{tinfo.time}}</div>
              <div>{{tinfo.weather}}</div>
              <div>{{tinfo.temp}}<span>℃</span></div>
            </div>
          </li>
        </ul>
      </div>
      <div class="next">
        <ul>
          <li v-for="ninfo in weatherinfo1.daily" class="ninfo">
            <div class="nweek">{{ninfo.week}}</div>
            <div class="nweather">{{ninfo.day.weather}}</div>
            <div class="nth">{{ninfo.day.temphigh}}</div>
            <div class="ntl">{{ninfo.night.templow}}</div>
          </li>
        </ul>
      </div>
      <div class="tdes">
        今天：当前 {{weatherinfo1.weather}}。气温 {{weatherinfo1.temp}}<span>℃</span>；最高气温
        {{weatherinfo1.temphigh}}<span>℃</span>。
      </div>
      <div class="otherinfo">
        <ul>
          <li>日出：{{weatherinfo1.daily[0].sunrise}}</li>
          <li>日落：{{weatherinfo1.daily[0].sunset}}</li>
          <li>湿度：{{weatherinfo1.humidity}}%</li>
          <li>风速：{{weatherinfo1.winddirect}} 每秒{{weatherinfo1.windspeed}}米</li>
          <li>气压：{{weatherinfo1.pressure}}百帕</li>
          <li>PM2.5：{{weatherinfo1.aqi.ipm2_5}}</li>
          <li>空气质量指数：{{weatherinfo1.aqi.aqi}}</li>
          <li>空气质量：{{weatherinfo1.aqi.quality}}</li>
          <li>影响：{{weatherinfo1.aqi.aqiinfo.affect}}</li>
          <li>建议：{{weatherinfo1.aqi.aqiinfo.measure}}</li>
        </ul>
      </div>
    </div>

  </div>
</template>

<script>
  import {Indicator} from 'mint-ui';

  export default {
    data () {
      return {
        url0: 'http://topTMZ.top:8080/tmz/weather/info',
        city: '上海',
        weatherinfo1: {},
        weatherinfo: {
          "city": "",
          "cityid": "",
          "citycode": "",
          "date": "",
          "week": "",
          "weather": "",
          "temp": "",
          "temphigh": "",
          "templow": "",
          "img": "",
          "humidity": "",
          "pressure": "",
          "windspeed": "",
          "winddirect": "",
          "windpower": "",
          "updatetime": "",
          "index": [
            {
              "iname": "空调指数",
              "ivalue": "部分时间开启",
              "detail": "您将感到些燥热，建议您在适当的时候开启制冷空调来降低温度，以免中暑。"
            },
            {
              "iname": "运动指数",
              "ivalue": "较不宜",
              "detail": "有降水，推荐您在室内进行低强度运动；若坚持户外运动，须注意携带雨具。"
            },
            {
              "iname": "紫外线指数",
              "ivalue": "中等",
              "detail": "属中等强度紫外线辐射天气，外出时建议涂擦SPF高于15、PA+的防晒护肤品，戴帽子、太阳镜。"
            },
            {
              "iname": "感冒指数",
              "ivalue": "少发",
              "detail": "各项气象条件适宜，发生感冒机率较低。但请避免长期处于空调房间中，以防感冒。"
            },
            {
              "iname": "洗车指数",
              "ivalue": "不宜",
              "detail": "不宜洗车，未来24小时内有雨，如果在此期间洗车，雨水和路上的泥水可能会再次弄脏您的爱车。"
            },
            {
              "iname": "空气污染扩散指数",
              "index": "良",
              "detail": "气象条件有利于空气污染物稀释、扩散和清除，可在室外正常活动。"
            },
            {
              "iname": "穿衣指数",
              "ivalue": "炎热",
              "detail": "天气炎热，建议着短衫、短裙、短裤、薄型T恤衫等清凉夏季服装。"
            }
          ],
          "aqi": {
            "pm2_5": "89",
            "aqi": "166",
            "primarypollutant": "O3",
            "quality": "中度污染",
            "timepoint": "2017-08-07 20:00:00",
            "aqiinfo": {
              "level": "四级",
              "color": "#FF0000",
              "affect": "",
              "measure": ""
            }
          },
          "daily": [
            {
              "date": "",
              "week": "",
              "sunrise": "",
              "sunset": "",
              "night": {
                "weather": "",
                "templow": "",
                "img": "1",
                "winddirect": "西南风",
                "windpower": "微风"
              },
              "day": {
                "weather": "",
                "temphigh": "",
                "img": "4",
                "winddirect": "西南风",
                "windpower": "微风"
              }
            }
          ],
          "hourly": [
            {
              "time": "",
              "weather": "",
              "temp": "",
              "img": ""
            }
          ]
        }
      }
    },
    watch: {},
    mounted: function () {
      this.getweather(this.url0);
    },
    methods: {
      getweather: function (url) {
        Indicator.open();
        setTimeout(() => {
          this.$http.post(url, {'city': this.city}, {emulateJSON: true})
            .then(
              (data) => {
                Indicator.close();
                console.log(data);
                this.weatherinfo1 = data.body.data;
              },
              (error) => {
                console.log(error);
              }
            );
        }, 300)
      }
    }
  }
</script>

<style>

  .now {
    /*border: solid 1px red;*/
    height: 220px;
    color: black;
    font-size: 20px;
    border-bottom: solid gray 1px;

  }

  .addr {
    /*border: solid 1px red;*/
    height: 40px;
    margin-top: 20px;
    line-height: 40px;
    color: black;
    font-size: 30px;
  }

  .winfo {
    /*border: solid 1px red;*/
    height: 20px;
    line-height: 20px;
    color: black;
    font-size: 16px;
  }

  .temp {
    /*border: solid 1px red;*/
    height: 80px;
    line-height: 80px;
    /*margin-top: 6px;*/
    color: black;
    font-size: 80px;
  }

  .temp span {
    height: 60px;
    line-height: 60px;
    color: black;
    font-size: 30px;
  }

  .nowinfo {
    margin-top: 16px;
  }

  .week {
    /*border: solid 1px red;*/
    height: 16px;
    line-height: 16px;
    color: black;
    font-size: 16px;
    float: left;
    margin-top: 40px;
    margin-left: 16px;
  }

  .t1t2 {
    /*border: solid 1px red;*/
    height: 16px;
    line-height: 16px;
    color: black;
    font-size: 16px;
    float: right;
    margin-top: 40px;
    margin-right: 16px;
  }

  .todayinfo {
    /*border: solid 1px red;*/
    height: 100px;
    width: 100%;
    border-bottom: solid gray 1px;

  }

  .todayinfo ul {
    height: 100px;
    list-style-type: none;
    display: -webkit-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
    -webkit-flex-wrap: nowrap;
    -ms-flex-wrap: nowrap;
    flex-wrap: nowrap;
    -webkit-box-pack: justify;
    -webkit-justify-content: space-between;
    -ms-flex-pack: justify;
    justify-content: space-between;
    /*background:#FF4878;*/
    padding: 0;
    overflow: auto;
  }

  .todayinfo ul li {
    -webkit-box-flex: 1;
    -webkit-flex: 1;
    -ms-flex: 1;
    flex: 1;
    height: 100px;
    line-height: 100px;
  }

  .tinfo {
    height: 100px;
    overflow-x: scroll;
    overflow-y: hidden;
  }

  .tinfo div {
    text-align: center;
    display: block;
    width: 3em;
    height: 20px;
    color: black;
    font-size: 16px;
    line-height: 20px;
    margin: 10px 6px;
  }

  .tinfo div span {
    font-size: 10px;
    color: black;
  }

  .tmzbody1 ul li {
    display: flex;
    float: left;
    /*border: solid 1px red;*/
    list-style-type: none;
    border-bottom: none;
    width: 100%;
  }

  .next {
    /*border: solid 1px red;*/
    height: 252px;
    border-bottom: solid gray 1px;
  }

  .next ul {

  }

  .next ul li {
    height: 36px;
    line-height: 36px;
    text-decoration: none;
  }

  .ninfo div {
    font-size: 16px;
    color: black;
    /*margin: 0 16px;*/
  }

  .nweek {
    position: absolute;
    left: 16px;
  }

  .nweather {
    position: relative;
    /*margin-left: 28%;*/
    margin-left: auto;
    margin-right: auto;
    text-align: center;
  }

  .nth {
    position: absolute;
    right: 56px;
  }

  .ntl {
    position: absolute;
    right: 24px;
    /*margin-right: 16px;*/
  }

  .tdes {
    height: 70px;
    /*border: solid 1px red;*/
    border-bottom: solid gray 1px;
    color: black;
    line-height: 35px;
    font-size: 20px;
    text-align: left;
    padding: 0 16px;
  }

  .tdes span {
    color: black;
    font-size: 16px;
  }

  .otherinfo {
    height: 200px;
    /*border: solid 1px red;*/
  }

  .otherinfo ul {
    width: 100%;
  }

  .otherinfo ul li {
    display: block;
    width: 100%;
    height: 30px;
    font-size: 20px;
    line-height: 30px;
    overflow: auto;
    text-align: center;
  }
</style>
