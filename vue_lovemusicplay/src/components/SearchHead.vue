<template>
  <div class="searchHead">
    <a-icon type="search" class="searchIcon"></a-icon>
    <form action="javascript:return true">
      <input type="search" @keyup.13="search()" class="searchInput" @click="switchPage('/search')" v-focus="PAGE" ref="seachInput">
    </form>
    <a-icon type="close" v-if="showCancelBtn()" class="cancelBtn" @click="switchPage('/')"></a-icon>
  </div>
</template>

<script>
import Vue from "vue";
import { Icon } from "ant-design-vue";
Vue.use(Icon);

export default {
  name: "searchHead",
  data () {
    return {
      PAGE: window.location.pathname//获取当前页面url,放回一个'/',或者"/search"
    }
  },
  methods: {
    search () {
      this.$refs.seachInput.blur();//让搜索框失去焦点
      const value = this.$refs.seachInput.value;//获取搜索的值，付给一个变量
      this.$emit('searchRes', value)//search()触发后，自动触发searchRes事件，该事件在父组件中,并发送value
    },
    switchPage (page) {
      this.$router.push(page);
    },//点击了输入框都会调用这个切换页面的方法
    showCancelBtn () {
      if (this.PAGE === "/search") {
        return true
      }
    }//控制“X"符号显示的方法，如果当前页面在search页，则显示取消返回的符号
  },
  directives: {
    focus: {
      // 在search页的时候 自动聚焦input
      inserted: function (el, { value }) {
        value === "/search" && el.focus();
      }
    }
  }
}
</script>

<style lang="less" scoped>
.searchHead {
  width: 100%;
  height: 2.5rem;
  background: #f1f1f1;
  border-radius: 2rem;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  & > form {
    width: 100%;
    height: 100%;
  }
  .searchIcon {
    font-size: 18px;
    margin-left: 1rem;
    font-weight: bold;
    color: #5b79ce;
  }
  .searchInput {
    width: 100%;
    height: 100%;
    font-size: 14px;
    padding: 10px;
    outline: 0;
    border: 0;
    background: transparent;
  }
  .cancelBtn {
    font-size: 18px;
    /* color: #6f6f6f; */
    margin-right: 1rem;
  }
}
</style>
