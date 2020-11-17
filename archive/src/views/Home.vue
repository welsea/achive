<template>
  <div class="home">
    <UserInfo />
    <div class="mainContent">
      <Timeline style="width:70%" />
      <div>
        <el-dropdown trigger="click" @command="handleCommand">
        <el-button type="primary" icon="el-icon-edit" plain >添加新条目</el-button>
          <el-dropdown-menu>
            <el-dropdown-item command="1" icon="el-icon-reading">阅读记录</el-dropdown-item>
            <el-dropdown-item command='2' icon="el-icon-film">观影记录</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
        <Tag />
      </div>
    </div>
  </div>
</template>

<script>
  // @ is an alias to /src
  import Timeline from '@/components/Timeline.vue'
  import UserInfo from '@/components/UserInfo.vue'
  import Tag from '@/components/Tag.vue'


  export default {
    name: 'Home',
    components: {
      Timeline,
      UserInfo,
      Tag
    },
    data() {
      return {
        type:'1'
      }
    },
    methods: {
      handleCommand(command){
        this.type=command;
        this.$router.push({
          path:'/add',
          query:{
            type:this.type
          }
        })
      }
    },
  }
</script>
<style>
  .mainContent {
    display: flex;
    align-items: flex-start;
  }
</style>