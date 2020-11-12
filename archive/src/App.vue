<template>
  <div id="app">
    <Header v-show="!(path==='/login')"></Header>
    <router-view></router-view>

  </div>
</template>

<script>
  import Header from './components/Header'
  export default {
    name: 'app',
    components: {
      Header
    },
    data() {
      return {
        path: ''
      }
    },
    methods: {
      changePath(to, from) {
        if (from.path === '/login') {
          this.path = to.path;
          console.log(to.path)
        }
      }
    },
    mounted() {
      this.path = this.$route.path;
    },
    watch: {
      $route(to, from) {
        this.changePath(to, from);
      }
    }
  }
</script>

<style>
  body {
    padding: 0;
    margin: 0;
  }
</style>