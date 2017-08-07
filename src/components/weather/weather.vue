<template>
    <div id="weather">
        <div class="tmzhead">
            <div class="tmzheadtitle">
                天气
            </div>
        </div>
      <div class="tmzbody">
        <div class="now"></div>
        <div class="next"></div>
        <div class="ninfo"></div>
      </div>

    </div>
</template>

<script>
    export default {
        data () {
            return {
                msg: 'weather'
            }
        }
    }
</script>

<style>

.now,.next,.ninfo{
    border: solid 1px red;
    height: 300px;
    /*margin: 6px 40px;*/
}
</style>
