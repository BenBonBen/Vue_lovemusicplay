<template>
  <div class="MusicFoot">
    <div class="song_img" @click="switchPage('/musicplay')">
      <img :src="musicdata.img" alt="">
    </div>
    <div class="song_msg" @click="switchPage('/musicplay')">
      <div class="singer_name">{{musicdata.song_name}}</div>
      <div class="song_name">{{musicdata.author_name}}</div>
    </div>
    <div class="song_bar">
      <a-icon :type="istrue?'play-circle':'pause-circle'" class="playBtn" @click="play" />
      <a-icon type="bars" class="playList" />
    </div>
    <audio id="music" :src="musicdata.play_url" autoplay="autoplay"></audio>
  </div>
</template>

<script>
import Vue from "vue";
import { Icon } from "ant-design-vue";
Vue.use(Icon);
export default {
  name: "MusicFoot",
  props: ['musicdata'],
  data () {
    return {
      PAGE: window.location.pathname,
      isPlaying: false, //控制歌曲的播放暂停
      istrue: ''
    }
  },
  methods: {
    switchPage (page) {
      this.$router.push(page)
    },
    play () {
      var audio = document.querySelector('#music');
      if (!this.isPlaying) {
        audio.play();
        this.isPlaying = true;
        this.istrue = false;
      } else {
        audio.pause();
        this.isPlaying = false;
        this.istrue = true;
      }
    },
    watch: {
      istrue: function () {
        var audio = document.querySelector('#music');
        if (audio.currentTime > 0) {
          this.istrue = false
        }
      }
    }
  },
}
</script>

<style lang="less">
.MusicFoot {
  width: 100%;
  height: 4rem;
  background-color: white;
  position: fixed;
  bottom: 0;
  left: 0;
  display: flex;
  .song_img {
    // width: 20%;
    display: flex;
    flex-basis: 15%;
    img {
      width: 100%;
      border-radius: 50%;
    }
  }
  .song_msg {
    flex-basis: 63%;
    padding-left: 3%;
    align-self: center;
  }
  .song_bar {
    display: flex;
    align-content: center;
    flex-basis: 22%;
    color: #5b79ce;
    .playBtn {
      font-size: 35px;
      align-self: center;
      flex-grow: 1;
    }
    .playList {
      font-size: 35px;
      align-self: center;
      flex-grow: 1;
    }
  }
}
</style>
