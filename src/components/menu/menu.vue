<template>
  <div>
    <div id="menu">
      <mu-paper id="mu-paper">
        <mu-bottom-nav :value="bottomNav" shift @change="handleChange" id="mu-bottom-nav">
          <mu-bottom-nav-item value="news" title="新闻" icon="subject"/>
          <mu-bottom-nav-item value="weather" title="天气" icon="music_note"/>
          <mu-bottom-nav-item value="plan" title="计划" icon="list"/>

          <mu-bottom-nav-item value="my" title="我的" icon="list"/>
        </mu-bottom-nav>
      </mu-paper>
    </div>
    <div v-if="bottomNav === 'news'">
      <news></news>
    </div>

    <div v-if="bottomNav === 'weather'">
      <weather></weather>
    </div>
    <div v-if="bottomNav === 'my'">
      <my></my>
    </div>
    <div v-if="bottomNav === 'plan'">
      <plan></plan>
    </div>
  </div>
</template>

<script>
  import news from '../news/news.vue'
  import weather from '../weather/weather.vue'
  import my from '../my/my.vue'
  import plan from '../plan/plan.vue'
  import test from '../news/test.vue'

  export default {
    data () {
      return {
        bottomNav: 'news',
        bottomNavColor: 'news'
      }
    },
    methods: {
      handleChange (val) {
        this.bottomNav = val
      }
    },
    components: {
      news,
      weather,
      my,
      plan,
      test
    }
  }
</script>

<style>
  #menu {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    z-index: 30;
  }

</style>
