<template>
  <div class="search page">
    <SearchHead @searchRes="getSearchWord" />
    <div class="musicList" v-for="searchData in searchDatas" v-bind:key='searchData.albumid'>
      <a-icon type="customer-service" theme="filled" class="musicIcon"></a-icon>
      <div class="musicmsg" @click="getsongmsg(searchData.FileHash,searchData.AlbumID)">
        <h3>
          {{searchData.songname}}
        </h3>
        <span>
          {{searchData.singer[0].name}}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import SearchHead from "@/components/SearchHead.vue";
import Vue from "vue";
import { Icon } from "ant-design-vue";
Vue.use(Icon);
import axios from "axios";

export default {
  name: "search",
  data () {
    return {
      searchDatas: [],//储存搜索结果
      musicdetail: {} //储存被选歌曲信息
    };
  },
  components: {
    SearchHead
  },
  methods: {
    // 获取搜索结果
    getSearchResult (word, page = 1, pagesize = 20) {
      axios
        .get("/soso/fcgi-bin/client_search_cp", {
          params: {
            aggr: 1,
            cr: 1,
            flag_qc: 0,
            w: word,
            p: page,
            n: pagesize
          }
        })
        .then(res => {
          this.searchDatas = this.stringtoJSON(res.data).data.song.list;
        });
    },
    getSearchWord (msg) {
      this.getSearchResult(msg);//接到由searchHead页面发过来的值，并且调用搜索方法
    },
    stringtoJSON (data) {
      if (typeof data === "string") {
        return JSON.parse(data.replace(/^callback\(/g, "").replace(/\)$/g, ""));
      }
      return data;
    },
    getsongmsg (hash, album_id) {
      axios.get("/yy/index.php?r=play/getdata&_=1497972864535&hash=", {
        params: {
          hash: hash,
          album_id: album_id
        }
      }).then(req => {
        this.musicdetail = this.stringtoJSON(req.data);
      })
    }
  }
};
</script>

<style lang="less">
.page {
  width: 100%;
  height: 100%;
  .musicList {
    display: flex;
    border-bottom: 1px solid gainsboro;
    .musicIcon {
      flex-basis: 8%;
      display: flex;
      align-items: center;
    }
    .musicmsg {
      flex-basis: 92%;
    }
  }
}
</style>
