<template>
  <div class="search page">
    <SearchHead @searchRes="getSearchWord" />
    <div class="totallist">
      <div class="musicList" v-for="searchData in searchDatas" v-bind:key='searchData.albumid'>
        <a-icon type="customer-service" theme="filled" class="musicIcon"></a-icon>
        <div class="musicmsg" @click="getsongmsg(searchData.FileHash,searchData.AlbumID)">
          <h3>
            {{searchData.SongName}}
          </h3>
          <span>
            {{searchData.SingerName}}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SearchHead from "@/components/SearchHead.vue";
import eventBus from "../eventBus.js";
import Vue from "vue";
import { Icon } from "ant-design-vue";
Vue.use(Icon);
import axios from "axios";

export default {
  name: "search",
  data () {
    return {
      searchDatas: [],//储存搜索结果
    };
  },
  components: {
    SearchHead,
  },
  methods: {
    // 获取搜索结果
    getSearchResult (word, page = 1) {
      axios
        .get("/search/song_search_v2", {
          params: {
            userid: parseInt(Math.random() * 100),
            clientver: '',
            platform: 'WebFilter',
            tag: 'em',
            filter: '2',
            iscorrection: '1',
            privilege_filter: 0,
            keyword: word,
            page: page
          }
        })
        .then(res => {
          this.searchDatas = this.checkString(res.data.data).lists;
        });
    },
    getSearchWord (msg) {
      this.getSearchResult(msg);//接到由searchHead页面发过来的值，并且调用搜索方法
    },
    checkString (data) {
      for (let i = 0; i < data.lists.length; i++) {
        const str = data.lists[i].SingerName
        const nameStr = data.lists[i].SongName
        //数据中存在<em>歌名</em>的现象，所以要把em标签去掉
        if (str.indexOf('<em>') !== -1 && str.indexOf('<em>') !== '-1') {
          let formatStr =
            str.slice(0, str.indexOf('<em>')) +
            str.slice(str.indexOf('<em>') + 4, str.indexOf('</em>')) +
            str.slice(str.indexOf('</em>') + 5)
          data.lists[i].SingerName = formatStr
        } else if (
          nameStr.indexOf('<em>') !== -1 &&
          nameStr.indexOf('<em>') !== '-1'
        ) {
          let formatName =
            nameStr.slice(0, nameStr.indexOf('<em>')) +
            nameStr.slice(
              nameStr.indexOf('<em>') + 4,
              nameStr.lastIndexOf('</em>')
            ) +
            nameStr.slice(nameStr.indexOf('</em>') + 5)
          data.lists[i].SongName = formatName
        }
      }
      return data
    },
    getsongmsg (hash, album_id) {
      axios.get("/kugou/yy/index.php?r=play/getdata&_=1497972864535&hash=", {
        params: {
          hash: hash,
          album_id: album_id
        }
      }).then(req => {
        this.musicdetail = req.data.data;
        eventBus.$emit('footerData', this.musicdetail)
      })
    },
  }
};
</script>

<style lang="less">
.search {
  width: 100%;
  height: 100%;
  overflow: scroll;
  .totallist {
    margin-bottom: 12%;
    .musicList {
      height: 54px;
      display: flex;
      border-bottom: 1px solid gainsboro;
      .musicIcon {
        flex-basis: 8%;
        display: flex;
        align-items: center;
        overflow: hidden;
      }
      .musicmsg {
        flex-basis: 92%;
        overflow: hidden;
      }
    }
  }
}
</style>
