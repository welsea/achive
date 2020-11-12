<template>
  <div>
    <div class="userinfo">
      <div class="status">加入于2020.10.11</div>
      <div class="info">
        <img src="../assets/avatar.png" alt="avatar" class="avatar">
        <div>
          <div class="name">welsea</div>
          <div class="id">@welsea@welsea.site</div>
        </div>
        <el-button class="setting" type="primary" @click="setting">设置</el-button>
      </div>

    </div>

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
    margin-bottom: 1em;
    padding: 1em 4em 0.5em 4em;
    border-width: 0 0 2px 0;
    border-style: dashed;
    border-color: #ddd;
  }

  .status {
    color: #ddd;
    /* position: relative; */
    /* right: 0; */
    text-align: right;
    font-size:0.9em;
  }

  .info {
    display: flex;
    align-items: flex-end;
    flex-direction: row;
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
    right: 4em;
  }
</style>