<template>
  <v-app id="inspire" light>
    <Navigation></Navigation>
    <Toolbar></Toolbar>
    <main>
      <v-content>
        <v-container fluid fill-height>
          <router-view></router-view>
        </v-container>
      </v-content>
    </main>
    <VFooter></VFooter>
    <!-- 信息提示 -->
    <v-snackbar
      :timeout="timeout"
      :color="toastsMsg.color"
      top
      v-model="toastsMsg.show"
    >
      {{ toastsMsg.text }}
    </v-snackbar>
  </v-app>
</template>

<script>
import Navigation from '@/components/AppView/Navigation'
import VFooter from '@/components/AppView/Footer'
import Toolbar from '@/components/AppView/Toolbar'
import EventBus from './eventbus'
// import fs from 'fs'
export default {
  data: () => ({
    serverList: [],
    timeout: 3000,
    port: '',
    toastsMsg: {
      show: false,
      color: 'error',
      text: ''
    }
  }),

  components: {
    Navigation,
    VFooter,
    Toolbar
  },

  mounted () {
    // 全局提示框，通过事件总线传递内容
    // EventBus.$emit('message', {show: true, color: 'error', text: 'some messages'})
    EventBus.$on('message', (message) => {
      this.toastsMsg = message
    })
    // 将开启的服务器保存在全局事件总线中
    EventBus.$on('createServer', (server) => {
      EventBus.$data.mockServerList.push(server)
    })
  },

  created () {
    // 在较早的加载事件中检查数据库与连接数据库

  }
}
</script>

<style lang="stylus">
@import './assets/stylus/main.styl';
</style>


<style>
@import url('./assets/font.css');
html::-webkit-scrollbar,
.hidden-scrollbar::-webkit-scrollbar {display:none}

/* Global CSS */
</style>
