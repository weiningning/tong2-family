<template>
<header class="top-container">
  <div class="top-bar clearfix">
    <div class="topbar-nav">
      <ul class="nav-wrap">
        <li class="nav">一个班主任对学生做的小调查与数据分析</li>
      </ul>
    </div>
    <div v-if="hasLogin" class="topbar-info">
      <span>{{user.name}}欢迎你</span>
      <span>|</span>
      <button v-on:click="toLogout">退出</button>
    </div>
    <div v-else class="topbar-info">
      <button v-on:click="toLogin">登录</button>
    </div>
  </div>
</header>
</template>

<script>
  import { mapActions } from 'vuex'
  // import { mapState } from 'vuex'
  export default {
    data() {
      return {
        user: {},
        hasLogin: this.$store.state.user.hasLogin
      }
    },
    computed: { 
      hasLogin() {
        return this.$store.state.login.hasLogin ? this.$store.state.login.hasLogin : this.$store.state.user.hasLogin
      },
      user() {
        return this.$store.state.user
      }
    },
    methods: {
      ...mapActions(['enableLogin', 'logOut', 'loginFail']),
      toLogin() {
        // this.islogin = true;
        // // 给父组件传递信息
        // this.$parent.$emit('to-login', { text: this.islogin})  
        this.enableLogin()
      },
      toLogout() {
        this.logOut()
        this.loginFail()
        this.$router.replace({path: '/'})
      }
    }
  }
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
.top-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 60px;
  background-color: #fff;
  box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12);
  z-index: 100;
  font-family: "Microsoft Yahei", sans-serif;
}
.topbar-nav {
  float: left;
  margin-left: 40px;
  display: inline-block;
  height: 60px;
  line-height: 60px;
  overflow: hidden;
}
.nav {
  font-size: 20px;
}
.topbar-info {
  position: absolute;
  top: 0;
  right: 40px;
  height: 60px;
  line-height: 60px;
}
button {
  color: #919191;
  font-size: 16px;
  border: none;
  background-color: #fff;
}
button:hover {
  color: #000;
}
.topbar-info span {
  color: #919191;
}
</style>
