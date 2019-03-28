<template>
  <div id="app">
    <router-view />
    <Musicplayfoot :musicdata='musicdetail' />
  </div>
</template>

<script>
import Musicplayfoot from "./components/Musicplayfoot.vue";
import eventBus from "./eventBus"

export default {
  data () {
    return {
      musicdetail: this.getmsgData() || {
        author_name: "张国荣",
        song_name: "张国荣 - 倩女幽魂 (粤语)",
        img: "http://imge.kugou.com/stdmusic/20160908/20160908170515309532.jpg",
        play_url: "http://fs.w.kugou.com/201903271224/a1fb767cea0e3742bc8e6f3a211185ba/G014/M05/0F/18/roYBAFUYMiiAVqhwADREFn04rIA343.mp3"
      },
    }
  },
  components: {
    Musicplayfoot
  },
  methods: {
    getmsgData () {
      eventBus.$on('footerData', (message) => {   //这里最好用箭头函数，不然this指向有问题
        return this.musicdetail = message
      })
    },
  }
}
</script>

<style>
/*公共样式--开始*/
html,
body,
div,
ul,
li,
h1,
h2,
h3,
h4,
h5,
h6,
p,
dl,
dt,
dd,
ol,
form,
input,
textarea,
th,
td,
select {
  margin: 0;
  padding: 0;
}
* {
  box-sizing: border-box;
}
html,
body {
  height: 100%;
  width: 100%;
}
body {
  font-family: 'Microsoft YaHei';
  font-size: 14px;
  color: #333;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  font-weight: normal;
}
ul,
ol {
  list-style: none;
}
img {
  border: none;
  vertical-align: middle;
}
a {
  text-decoration: none;
  color: #232323;
}
table {
  border-collapse: collapse;
  table-layout: fixed;
}
input,
textarea {
  outline: none;
  border: none;
}
textarea {
  resize: none;
  overflow: auto;
}
.clearfix:after {
  content: '';
  height: 0;
  visibility: hidden;
  display: block;
  clear: both;
}
.clearfix {
  zoom: 1;
}
.fl {
  float: left;
}
.fr {
  float: right;
}
.tl {
  text-align: left;
}
.tc {
  text-align: center;
}
.tr {
  text-align: right;
}
.ellipse {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.inline {
  display: inline-block;
  *display: inline;
  *zoom: 1;
}

#app {
  width: 100%;
  height: 100%;
  overflow-x: hidden;
}
</style>
