<template>
    <div class="addRead">
        <div class="setp1" v-show="step==1">
            <div style="margin-bottom:1em;">
                <el-radio-group v-model="type" @change="typeChange">
                    <el-radio :label="1">新建</el-radio>
                    <el-radio :label="2">添加已有</el-radio>
                </el-radio-group>
            </div>

            <div class="new">
                <div>
                    搜索已有条目
                    <el-autocomplete class="inline-input" v-model="exit" :fetch-suggestions="querySearch"
                        placeholder="请输入内容" @select="handleSelect"></el-autocomplete>
                </div>
                <div>书名<el-input v-model="basicInfo.title" clearable style="width:200px; margin-left:1em"
                        :disabled="type==2"></el-input>
                </div>
                <div>作者<el-input v-model="basicInfo.author" clearable style="width:200px; margin-left:1em"
                        :disabled="type==2"></el-input>
                </div>
                <div>开始时间<el-date-picker style=" margin-left:1em" v-model="basicInfo.start" type="date"
                        placeholder="选择日期" format="yyyy 年 MM 月 dd 日" value-format="yyyy-MM-dd" :disabled="type==2">
                    </el-date-picker>
                </div>
                <div>
                    状态
                    <el-radio-group v-model="basicInfo.status" @change="statusChange">
                        <el-radio :label="1" style=" margin-left:1em">已读完</el-radio>
                        <el-radio :label="2">未读完</el-radio>
                    </el-radio-group>
                </div>
                <div>
                    <AddTags v-on:tags="tags" v-if="type==1" />
                    <AddTags :exit_tags="basicInfo.tag" v-else />
                </div>
            </div>
        </div>
        <div class="step2" v-show="step==2">step2</div>
        <div class="nextbtn">
            <el-button type="primary" @click="nextStep">Next</el-button>
        </div>
    </div>

</template>
<script>
    import AddTags from '@/components/AddTags.vue'
    export default {
        name: 'addRead',
        components: {
            AddTags
        },
        data() {
            return {
                type: 1,
                basicInfo: {
                    title: '',
                    author: '',
                    start: '',
                    status: 1,
                    tag: []
                },
                title: '',
                author: '',
                start: '',
                status: 1,
                exit: '',
                exited_records: [],
                step: 1,
                step1:false
            }
        },
        methods: {
            typeChange(val) {
                this.type = val;
            },
            statusChange(val) {
                this.basicInfo.status = val;
            },
            querySearch(queryString, cb) {
                var exited_records = this.exited_records;
                var results = queryString ? exited_records.filter(this.createFilter(queryString)) : exited_records;
                // 调用 callback 返回建议列表的数据
                cb(results);
            },
            createFilter(queryString) {
                return (exited_record) => {
                    console.log(exited_record.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0)

                    return (exited_record.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0);
                };
            },
            loadAll() {
                return [{
                        title: 'his dark materials',
                        value: 'his dark materials',
                        author: 'pullman',
                        start: '2020-10-20',
                        status: 2,
                        tag: ['sci-fic']
                    },
                    {
                        title: 'harry potter',
                        value: 'harry potter',
                        author: 'J.K',
                        start: '2020-10-19',
                        status: 2,
                        tag: ['sci-fic']
                    },
                    {
                        title: 'earthsea',
                        value: 'earthsea',
                        author: 'Usula',
                        start: '2020-10-18',
                        status: 2,
                        tag: ['sci-fic']
                    }
                ]
            },
            handleSelect(item) {
                this.basicInfo = item;
            },
            nextStep() {
                console.log(this.basicInfo);
                this.$emit(this.step1)
                this.step++
            },
            tags(tags) {
                tags.forEach(function (val, i) {
                    this.basicInfo.tag[i] = val;
                });
            }
        },
        mounted() {
            this.exited_records = this.loadAll()
        },
    }
</script>
<style scoped>
    .new>div {
        margin-bottom: 1em;
    }

    .nextbtn {
        text-align: right;
        margin-top: 6em;
        position: relative;
        right: -2em;
    }
</style>