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
            <el-dropdown-item command="read" icon="el-icon-reading">阅读记录
              <!-- <el-dropdown trigger="click" placement="bottom-start" @command="handleCommand2">
                <span><i class="el-icon-reading"></i>阅读记录</span>
                <el-dropdown-menu>
                  <el-dropdown-item command="new">新建记录</el-dropdown-item>
                  <el-dropdown-item command="exist">添加已有</el-dropdown-item>
                </el-dropdown-menu>
              </el-dropdown> -->
            </el-dropdown-item>
            <el-dropdown-item command='watch' icon="el-icon-film">观影记录</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
        <Tag />
      </div>
    </div>
    <el-dialog title="选择类型" :visible.sync="showDialog" width="30%">
      <el-radio-group v-model="type2" @change="typeChange">
        <el-radio :label="1" style=" margin-left:1em">新建记录</el-radio>
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
        }],
        showDialog: false,
        type:1,
        type2:1
      }
    },
    methods: {
      typeChange(val){
        this.type2=val;
      },
      chooseType(){
        let exist;
        if(this.type2==1){
          exist=false;
        }else{
          exist=true;
        }
        this.$router.push({
          name: 'Add',
          params: {
            type: '1',
            exist: exist
          }
        })
      },
      handleCommand(command) {
        if (command == 'watch') {
          this.$router.push({
            name: 'Add',
            params: {
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