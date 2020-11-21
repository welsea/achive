<template>
  <div class="home">
    <UserInfo />
    <div class="mainContent">
      <Timeline style="width:70%" />
      <div>
        <!-- <el-cascader v-model="value" :options="options" @change="selectType">
        </el-cascader> -->
        <el-dropdown trigger="click" @command="handleCommand">
          <el-button type="primary" icon="el-icon-edit" plain>添加新条目</el-button>
          <el-dropdown-menu>
            <el-dropdown-item command="read" icon="el-icon-reading">阅读记录</el-dropdown-item>
            <el-dropdown-item command='watch' icon="el-icon-film">观影记录</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
        <Tag />
      </div>
    </div>
    <el-dialog title="选择类型" :visible.sync="showDialog" width="30%">
      <el-radio-group v-model="exist" @change="typeChange">
        <el-radio :label="1" style="margin-left:1em">新建记录</el-radio>
        <el-radio :label="2">向已有记录添加</el-radio>
      </el-radio-group>
      <span slot="footer" class="dialog-footer">
        <el-button @click="showDialog=false">取消</el-button>
        <el-button type="primary" @click="chooseType">确定</el-button>
      </span>
    </el-dialog>
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
        showDialog: false,
        exist: 1,
      }
    },
    methods: {
      typeChange(val) {
        this.exist = val;
      },
      chooseType() {
        let e;
        if (this.exits == 1) {
          e = false;
        } else {
          e = true;
        }
        this.$router.push({
          path:'/add',
         query: {
            type: '1',
            exist: e
          }
        })
      },
      handleCommand(command) {
        if (command == 'watch') {
          this.$router.push({
            path:'/add',
            query: {
              type: '2',
            }
          })
        } else {
          this.showDialog = true;
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