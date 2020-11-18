<template>
  <div class="home">
    <UserInfo />
    <div class="mainContent">
      <Timeline style="width:70%" />
      <div>
        <el-cascader v-model="value" :options="options" @change="selectType">

        </el-cascader>
        <!-- <el-dropdown trigger="click" @command="handleCommand">
        <el-button type="primary" icon="el-icon-edit" plain >添加新条目</el-button>
          <el-dropdown-menu>
            <el-dropdown-item command="1" icon="el-icon-reading">阅读记录</el-dropdown-item>
            <el-dropdown-item command='2' icon="el-icon-film">观影记录</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown> -->
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
        value: [],
        options: [{
          value: 'read',
          label: '阅读记录',
          children: [{
            value: 'exist',
            label: '添加已有'
          }, {
            value: 'new',
            label: '新建记录'
          }]
        }, {
          value: 'watch',
          label: '观影记录'
        }]
      }
    },
    methods: {
      selectType(value) {
        if (value[0] == 'read') {
          if (value[1] == 'exist') {
            this.$router.push({
              name: 'Add',
              params: {
                type: '1',
                exist:true
              }
            })
          }else{
            this.$router.push({
              name: 'Add',
              params: {
                type: '1',
                exist:false
              }
            })
          }
        }else{
          this.$router.push({
              name: 'Add',
              params: {
                type: '2',
              }
            })
        }
        
      },
    },
    created() {
      
    },
  }
</script>
<style>
  .mainContent {
    display: flex;
    align-items: flex-start;
  }
</style>