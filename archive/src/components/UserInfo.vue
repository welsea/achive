<template>
  <div class="userinfo">
    <img src="../assets/avatar.png" alt="avatar" class="avatar">
    <div>
      <div class="name">welsea</div>
      <div class="id">@welsea@welsea.site</div>
    </div>
    <el-button class="setting" type="primary" @click="setting">设置</el-button>
  </div>
</template>

<script>
  export default {
    name: 'UserInfo',
    methods: {
      setting() {
        console.log('setting')
      }
    },

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .avatar {
    width: 6em;
    border-radius: 6em;
    position: relative;
    top: 1.3em;
    margin-right: 1em;
  }

  .userinfo {
    display: flex;
    align-items: flex-end;
    flex-direction: row;
    margin-bottom: 1em;
    padding: 2em 2em 0.5em 2em;
    border-width: 0 0 2px 0;
    border-style: dashed;
    border-color: #ddd;
  }

  .name {
    font-size: 0.9em;
  }

  .id {
    font-size: 0.8em;
    color: #888;
  }

  .setting {
    position: absolute;
    right: 1em;
  }
</style>