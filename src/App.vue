<template>
  <div id="app">
    <div v-if="!browser">
      {{ msg }}
    </div>
    <Redirect v-else :browser="browser" />
  </div>
</template>

<script>
import Redirect from './components/Redirect.vue'
const queryString = require('query-string');
const parsed = queryString.parse(window.location.search);

// 允许跳转的域名列表，留空则不限制
const allows = [];

export default {
  name: 'App',
  data () {
    return {
      msg: ''
    }
  },
  components: {
    Redirect
  },
  computed: {
    isWechat () {
      return (this.userAgent.match(/MicroMessenger/i) == "micromessenger") ? true : false;
    },
    /**
     * 是否内置浏览器
     * 
     * @return string|null
     * 微信返回 wechat
     * QQ返回 qq
     *
     * 如果不是内置浏览器，返回NULL
     */
    browser () {
      return this.isWechat ? 'wechat' : (this.isQQ ? 'qq' : null)
    },
    isQQ () {
      return (this.userAgent.match(/MQQBrowser/i) == "mqqbrowser") ? true : false;
    },
    userAgent () {
      return navigator.userAgent.toLowerCase();
    }
  },
  created () {
    let u = parsed.u;
    let url = parsed.url;

    if (!this.browser) {
      if (u) {
        u = window.atob(u);// base64解码URL
        let uobj = new URL(u)
        if (allows && allows.length && allows.indexOf(uobj.hostname) == -1) {
          return this.msg = '拒绝跳转该网址'
        }
        this.msg = '请稍候...';
        window.location.href = u;
      } else if (url) {
        let url_encode = '?u=' + window.btoa(url);
        prompt("参数为", url_encode)
        this.msg = '请复制参数'
      } else {
        this.msg = '缺少必要参数'
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  padding-top: 40px;
}
body {
  margin: 0;
  overflow: hidden;
}

</style>
