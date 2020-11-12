<template>
  <div class="timeline">
    <div class="timeline-top">
      <div class="type">
        <el-radio-group v-model="radio" @change="changeType">
          <el-radio-button label="ALL"></el-radio-button>
          <el-radio-button label="阅读"></el-radio-button>
          <el-radio-button label="影视剧"></el-radio-button>
        </el-radio-group>
      </div>
      <div class="search">
        <el-input placeholder="搜索条目" prefix-icon="el-icon-search" v-model="input">
        </el-input>
      </div>
    </div>
    <div class="side-tab">
      <el-tabs v-model="activeName" @tab-click="handleClick" tabPosition="right">
        <el-tab-pane v-for="year in years" :label="year" :name="year" :key="year">
          <div class="month">
            4.2020
          </div>
          <div class="detail">
            <el-timeline>
              <el-timeline-item v-for="(activity, index) in activities" :key="index" :icon="activity.icon"
                :type="activity.type" color="white" size="large" :timestamp="activity.timestamp">
                {{activity.content}}
              </el-timeline-item>
            </el-timeline>
          </div>
        </el-tab-pane>
      </el-tabs>
    </div>

  </div>
</template>

<script>
  export default {
    name: 'timeline',
    data() {
      return {
        radio: 'ALL',
        input: '',
        activeName: '',
        years: ['2020', '2019', '2018'],
        activities: [{
            content: '《厌女》阅读记录',
            timestamp: '04-12 20:46',
            icon: 'el-icon-reading'
          },
          {
            content: '《2049》',
            timestamp: '04-11 20:46',
            icon: 'el-icon-film'
          }
        ]
      }
    },
    methods: {
      handleClick(tab) {
        this.activeName = tab.label;
      },
      changeType(type) {
        console.log(type);
      }

    },
    created() {
      this.activeName = this.years[0];
    },

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .timeline {
    margin: 3em;
  }

  .timeline-top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: relative;
    top: -2.2em;
    left: 7em;
  }

  .search {
    width: 200px;
    /* position: relative; */
    /* top: -6em; */
    /* right: 2em; */
    margin-right: 7em;
  }

  .month {
    color: #888;
    margin-left: 9em;
    margin-bottom: 1em;
    font-size: 0.8em;
  }

  .detail {
    margin-left: 7em;
  }
</style>
<style>
  .el-icon-reading,
  .el-icon-film {
    color: #44a448 !important;
  }
</style>