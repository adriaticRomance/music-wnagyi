<template>
  <div id="app" @touchstart="touchstart" @touchend="touchend">
    
    <!-- 一级路由出口 -->
    <keep-alive>
    <router-view @tanslate-song-id='currentSongId = $event'></router-view>
    </keep-alive>
    <!-- 播放器 -->
    <audio src='currentSongUrl' v-if="currentSongUrl" controls autoplay style="height:36px"></audio>
  </div>
</template>
<script>
export default {
  data() {
    return {
      currentSongId:'',
      touchstartX:0
    }
  },
  
  computed: {
    currentSongUrl:function(){
      return `https://music.163.com/song/media/outer/url?id=${this.currentSongId}.mp3`
    }
  },
  methods: {
    touchstart:function(event){
      this.touchstartX = event.changedTouches[0].clientX
      this.touchstartY = event.changedTouches[0].clientY 
    },
    touchend:function(event){
      if(event.changedTouches[0].clientX - this.touchstartX>50){
        this.touchstartX = 0;
        this.touchstartY = 0;
        this.routerBack()
      }
    },
    routerBack:function(){
      this.$router.back()
    }
  },
  watch: {
    currentSongId:function(){

    } 
  }
}
</script>
<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>