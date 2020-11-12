<template>
  <div class="home">
    <UserInfo />
    <div class="mainContent">
      <Timeline style="width:70%" />
      <div>
        <el-button type="primary" icon="el-icon-edit" plain>添加新条目</el-button>
          
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
    }
  }
</script>
<style>
  .mainContent {
    display: flex;
    align-items: flex-start;
  }
</style>