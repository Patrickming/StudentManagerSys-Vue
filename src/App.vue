<!--
 * @Description: 
 * @Author: Rabbiter
 * @Date: 2023-03-03 20:03:53
-->
<template>
  <div id="app">
    <router-view v-if="isRouterAlive"></router-view>
  </div>
</template>

<script>
    export default {
        name: 'App',
      provide () {
        return {
          reload: this.reload
        }
      },
      data () {
        return {
          isRouterAlive: true
        }
      },
      methods: {
        reload () {
          this.isRouterAlive = false;
          this.$nextTick(function () {
            this.isRouterAlive = true
          })
        },
      },
      mounted () {
        
      },
      computed: {
        
      },
    }
</script>
<style>

  html, body {
    overflow-x: hidden;
  }
</style>
