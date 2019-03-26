<template>
  <div class="Musicplay page">
    <div class="player_head">
      <a-icon type="left" class="back" @click="switchPage('/')" />
      <div class="musicmsg">
        <div class="songname">张国荣-玻璃之情</div>
        <div class="singer">张国荣</div>
      </div>
      <a-icon type="fork" class="shall" />
    </div>
    <div class="musicPic">
      <img src="http://imge.kugou.com/stdmusic/20160907/20160907201817543618.jpg" alt="" id="imgurl">
    </div>
    <div class="function_bar">
      <a-icon type="heart" class="love" />
      <a-icon type="download" class="download" />
      <a-icon type="message" class="comment" />
      <a-icon type="folder-add" class="collect" />
    </div>
    <div class="timeBar">
      <div class="startTime">0:00</div>
      <div class="progressbar">
        <div class="progressing"></div>
      </div>
      <div class="endTime">4:00</div>
    </div>
    <div class="media_control">
      <a-icon type="retweet" class="playstyles" />
      <a-icon type="step-backward" class="icon-prev" />
      <a-icon type="play-circle" class="icon-play" />
      <a-icon type="step-forward" class="icon-next" />
      <a-icon type="menu-unfold" class="player-list" />
    </div>
    <audio id="music" src="http://fs.w.kugou.com/201903251429/f8ca656ce47010ee4d771225519e6a69/G027/M05/13/13/-5MEAFWe0WqADZf3AEQsNVDXp1E565.mp3"></audio>
  </div>
</template>

<script>
export default {
  methods: {
    switchPage (page) {
      this.$router.push(page);
    }
  }
}
</script>

<style lang="less" scoped>
.Musicplay {
  width: 100%;
  // height: 100%;
  // display: flex;
  .player_head {
    width: 100%;
    height: 3rem;
    display: flex;
    .back {
      flex-basis: 15%;
      font-size: 35px;
      color: #5b79ce;
      align-self: center;
    }
    .musicmsg {
      flex-basis: 70%;
      align-self: center;
      text-align: center;
    }
    .shall {
      flex-basis: 15%;
      font-size: 35px;
      color: #5b79ce;
      align-self: center;
    }
  }
  .musicPic {
    width: 80%;
    height: 18.64rem;
    display: flex;
    margin: 4rem auto;
    img {
      align-content: center;
      width: 100%;
      height: 100%;
      border-radius: 50%;
    }
  }
  .function_bar {
    width: 100%;
    height: 2rem;
    display: flex;
    .love {
      font-size: 30px;
      flex-basis: 25%;
      color: #5b79ce;
    }
    .download {
      font-size: 30px;
      flex-basis: 25%;
      color: #5b79ce;
    }
    .comment {
      font-size: 30px;
      flex-basis: 25%;
      color: #5b79ce;
    }
    .collect {
      font-size: 30px;
      flex-basis: 25%;
      color: #5b79ce;
    }
  }
  .timeBar {
    margin-top: 2rem;
    width: 100%;
    height: 2rem;
    display: flex;
    .startTime {
      width: 8%;
      flex-basis: 8%;
      align-self: center;
    }
    .progressbar {
      width: 84%;
      height: 5px;
      background: #eaeaea;
      align-self: center;
      flex-basis: 84%;
      .progressing {
        width: 0%;
        height: 100%;
        background: #3a6efd;
      }
    }
    .endTime {
      width: 8%;
      flex-basis: 8%;
      align-self: center;
    }
  }
  .media_control {
    margin-top: 3rem;
    width: 100%;
    height: 4rem;
    display: flex;
    .playstyles {
      align-self: center;
      font-size: 40px;
      flex-basis: 20%;
      color: #5b79ce;
    }
    .icon-prev {
      align-self: center;
      font-size: 40px;
      flex-basis: 20%;
      color: #5b79ce;
    }
    .icon-play {
      align-self: center;
      font-size: 40px;
      flex-basis: 20%;
      color: #5b79ce;
    }
    .icon-next {
      align-self: center;
      font-size: 40px;
      flex-basis: 20%;
      color: #5b79ce;
    }
    .player-list {
      align-self: center;
      font-size: 40px;
      flex-basis: 20%;
      color: #5b79ce;
    }
  }
}
</style>
