<template>
    <div class="addRead">
        <div class="btn">
            <button :class="[disabled? 'disabled':'nbtn']" :disabled="disabled" @click="priStep">上一步</button>
            <button class="nbtn" @click="nextStep">下一步</button>
        </div>
        <div class="title">创建新记录</div>
        <div class="step1" v-show="step==1">
            <!-- <div>添加新记录</div> -->
            <div style="margin-bottom:1em;">
                <el-form ref="basicInfo" :model="basicInfo" :rules="rules" label-width="7em">
                    <el-form-item v-show="ise" label="搜索已有条目">
                        <el-autocomplete class="inline-input" v-model="exit" :fetch-suggestions="querySearch"
                            placeholder="请输入内容" @select="handleSelect"></el-autocomplete>
                    </el-form-item>
                    <el-form-item label="书名" prop="name">
                        <el-input v-model="basicInfo.name" clearable style="width:200px; margin-left:1em"
                            :disabled="ise"></el-input>
                    </el-form-item>
                    <el-form-item label="作者" prop="author">
                        <el-input v-model="basicInfo.author" clearable style="width:200px; margin-left:1em"
                            :disabled="ise"></el-input>
                    </el-form-item>
                    <el-form-item label="开始时间" prop="start">
                        <el-date-picker style=" margin-left:1em" v-model="basicInfo.start" type="date"
                            placeholder="选择日期" format="yyyy 年 MM 月 dd 日" value-format="yyyy-MM-dd" :disabled="ise">
                        </el-date-picker>
                    </el-form-item>
                    <el-form-item label="状态">
                        <el-radio-group v-model="basicInfo.status" @change="statusChange">
                            <el-radio :label="1" style=" margin-left:1em">已读完</el-radio>
                            <el-radio :label="2">未读完</el-radio>
                        </el-radio-group>
                    </el-form-item>
                    <el-form-item label="添加标签">
                        <AddTags v-on:ch_tag="ch_tag" v-if="isShow" />
                        <AddTags :exit_tags="basicInfo.tag" v-else />
                    </el-form-item>
                </el-form>
            </div>
        </div>

        <div class="step2" style="width:70%; margin:auto;padding-bottom:2em" v-show="step==2">
            <div class="info">
                <i class="el-icon-reading icon"></i>
                <div class="main_info">
                    <div>{{basicInfo.name}}</div>
                    <div><span>作者：</span>{{basicInfo.author}}</div>
                </div>
                <div class="status_info">
                    <div><span>起始时间：</span>{{basicInfo.start}}</div>
                    <div><span>阅读状态：</span>{{(basicInfo.status==1)? '已读完':'未读完'}}</div>
                    <div v-show="basicInfo.tag.length!==0">
                        <span>标签：</span>
                        <div class="tag" v-for="(item,i) in basicInfo.tag" :key="i" effect="plain">#{{item}}</div>
                    </div>
                </div>
            </div>
            <div style="margin-bottom:1em">
                <el-input v-model="title" placeholder="请输入标题"></el-input>
            </div>
            <tinymce />
        </div>
        <!-- <div class="nextbtn">
            <el-button type="primary" @click="nextStep">Next</el-button>
        </div> -->
    </div>

</template>
<script>
    import AddTags from '@/components/AddTags.vue'
    import tinymce from '@/components/RichText.vue'

    export default {
        name: 'addRead',
        components: {
            AddTags,
            tinymce
        },
        data() {
            return {
                type: 1,
                basicInfo: {
                    name: '',
                    author: '',
                    start: '',
                    status: 1,
                    tag: [],
                },
                rules: {
                    name: [{
                        required: true,
                        message: '请输入书名',
                        trigger: 'change'
                    }],
                    author: [{
                        required: true,
                        message: '请输入作者',
                        trigger: 'change'
                    }],
                    start: [{
                        required: true,
                        message: '请选择时间',
                        trigger: 'change'
                    }],
                },
                exit: '',
                exited_records: [],
                step: 1,
                msg: 'use tinymce',
                disabled: true,
                isShow: false,
                title: '',
                ise: false
            }
        },
        props: {
            isExist: String
        },
        methods: {
            //step1
            resetForm(name) {
                this.$refs[name].resetFields();
                this.basicInfo.status = 1;
                this.basicInfo.tag = [];
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
                    return (exited_record.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0);
                };
            },
            loadAll() {
                return [{
                        name: 'his dark materials',
                        value: 'his dark materials',
                        author: 'pullman',
                        start: '2020-10-20',
                        status: 2,
                        tag: ['sci-fic']
                    },
                    {
                        name: 'harry potter',
                        value: 'harry potter',
                        author: 'J.K',
                        start: '2020-10-19',
                        status: 2,
                        tag: ['sci-fic']
                    },
                    {
                        name: 'earthsea',
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
            ch_tag(tags) {
                let ch_tags = []
                tags.forEach(function (val, i) {
                    ch_tags[i] = val;
                });
                this.basicInfo.tag = ch_tags;
            },
            nextStep() {
                if (this.submit()) {
                    this.step++
                    this.disabled = false;
                } else {
                    console.log(this.submit());
                    
                }
                if (this.step > 2) {
                    this.$router.push({
                        path: '/record',
                        query: {
                            type: 'read'
                        }
                    })
                }
                // console.log(this.submit())
            },
            submit() {
                let result;
                this.$refs['basicInfo'].validate((valid) => {
                    if(valid){
                        result=true
                    }else{
                        result=false
                    }
                })
                return result;
            },
            priStep() {
                if (this.step > 1) {
                    this.step--
                }
                if (this.step == 1) {
                    this.disabled = true;
                }
            },
            isE() {
                if (this.isExist == 'true') {
                    this.ise = true;
                } else {
                    this.ise = false;
                }
            }
            //step2

        },
        mounted() {
            this.exited_records = this.loadAll()
            this.isE();
        },
        created() {
            // this.isE();
        },
    }
</script>
<style scoped>
    .new>div {
        margin-bottom: 1em;
    }

    /* .nextbtn {
        text-align: right;
        margin-top: 6em;
        position: relative;
        right: -2em;
    } */

    .step1 {
        width: fit-content;
        margin: auto;
    }

    .new span {
        color: rgb(194, 11, 11);
    }

    .info span {
        color: #888;
    }

    .info>div {
        margin-bottom: 1em;
    }

    .main_info {
        display: flex;
        flex-direction: row;
        align-items: baseline;
        font-size: 0.9em;
    }

    .main_info div:first-child {
        font-size: 1.5em;
        margin-right: 1em;
    }

    .status_info {
        display: flex;
        flex-direction: row;
        font-size: 0.9em;
    }

    .status_info>div {
        margin-right: 2em;
    }

    .tag {
        display: inline-block;
        font-size: 0.7em;
        color: green;
        background-color: #69b66d1c;
        margin-left: 0.5em;
        padding: 2px;
        border-radius: 3px;
    }

    .icon {
        position: relative;
        right: 1.2em;
        font-size: 2em;
        top: 1em;
    }

    .btn {
        display: flex;
        justify-content: space-between;
        margin-bottom: 1em;
        background-color: #44a44710;
    }

    .btn button {
        border: none;
        padding: 0.6em 1.5em;
    }

    .nbtn {
        border: none;
        /* border-color:#44a448; */
        color: white;
        background-color: #44a448;
        padding: 0.6em 1.5em;
    }

    .title {
        width: fit-content;
        margin: auto;
        font-size: 2em;
        /* position: absolute; */
        /* left: 15em; */
        /* padding-bottom: 10px; */
        color: #2f964559;
    }

    .disabled {
        background-color: #888;
        color: white;
    }
</style>