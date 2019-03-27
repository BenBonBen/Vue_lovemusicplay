<template>
  <div class="home page">
    <SearchHead />
    <Banner :sliderData="recommendDatas.slider" />
    <div class="classification">
      <div class="classItem" v-for="(item, i) in classificationData" :key="i">
        <a-icon class="icon" :type="item.icon" />
        <div class="name">{{item.name}}</div>
      </div>
    </div>
    <div class="hotList">
      <div class="hotTitle">电台</div>
      <div class="hotMusic" v-for="hotData in recommendDatas.radioList" :key="hotData.radioid">
        <img :src="hotData.picUrl" class="hotmusic_pic" alt="">
        <div class="hotmusic_title">{{hotData.Ftitle}}</div>
      </div>
    </div>
    <div class="recommendList">
      <div class="recommendTitle">热门歌单</div>
      <div class="recommendMusic" v-for="(recommendData,i) in recommendDatas.songList" :key="i">
        <img :src="recommendData.picUrl" class="recommendMusic_pic" alt="">
        <div class="recommend_desc">{{recommendData.songListDesc}}</div>
        <div class="recommend_author">{{recommendData.songListAuthor}}</div>
        <div class="recommend_num">{{recommendData.accessnum/1000}}万</div>
      </div>
    </div>
    <Musicplayfoot :musicdata='musicdetail' />
  </div>
</template>

<script>
// @ is an alias to /src
import SearchHead from "@/components/SearchHead.vue";
import Banner from "@/components/Banner.vue";
import Musicplayfoot from "@/components/Musicplayfoot.vue";
import eventBus from "@/eventBus.js";
import axios from "axios";
import Vue from "vue";

import { Icon } from "ant-design-vue";
Vue.use(Icon);

export default {
  name: "home",
  components: {
    SearchHead,
    Banner,
    Musicplayfoot
  },
  data () {
    return {
      recommendDatas: {},
      classificationData: [
        { icon: "fire", name: "推荐" },
        { icon: "line-chart", name: "排行" },
        { icon: "rocket", name: "最新" },
        { icon: "customer-service", name: "电台" }
      ],
      musicdetail: {
      }//储存被选歌曲信息
    };
  },
  created: function () {
    this.fetchData();
  },
  mounted () {
    this.getmsgData()
  },
  methods: {
    fetchData () {
      axios
        .get("/qq/musichall/fcgi-bin/fcg_yqqhomepagerecommend.fcg")
        .then(res => {
          return (this.recommendDatas = res.data.data);
        });
    },
    getmsgData () {
      eventBus.$on('msgtoHome', (message) => {   //这里最好用箭头函数，不然this指向有问题
        this.musicdetail = message
      })
    }
  }
};
</script>

<style lang="less">
.page {
  width: 100%;
  height: 100%;
  padding: 5%;
  .classification {
    display: flex;
    justify-content: space-around;
    .classItem {
      .name {
        text-align: center;
        margin-top: 0.3rem;
      }
      .icon {
        font-size: 35px;
        color: #628bd8;
      }
    }
  }
  .hotList {
    width: 100%;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    padding-top: 2%;
    .hotTitle {
      width: 100%;
      display: flex;
      padding-bottom: 2%;
    }
    .hotMusic {
      width: 45%;
      display: flex;
      flex-direction: column;
      .hotmusic_pic {
        width: 100%;
        border-radius: 5%;
      }
    }
  }
  .recommendList {
    width: 100%;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    margin-bottom: 17%;
    .recommendTitle {
      width: 100%;
      display: flex;
      padding-top: 2%;
      padding-bottom: 2%;
    }
    .recommendMusic {
      width: 45%;
      display: flex;
      flex-direction: column;
      position: relative;
      .recommendMusic_pic {
        width: 100%;
        border-radius: 5%;
      }
      .recommend_desc {
        text-align: left;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
      }
      .recommend_author {
        color: black;
        text-align: left;
        font-weight: bolder;
      }
      .recommend_num {
        position: absolute;
        bottom: 20%;
        left: 5%;
        color: white;
      }
    }
  }
}
</style>
