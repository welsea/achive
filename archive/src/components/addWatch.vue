<template>
    <div class="addWatch">
        <div class="btn">
            <button :class="[disabled? 'disabled':'nbtn']" :disabled="disabled" @click="priStep">上一步</button>
            <button class="nbtn" @click="nextStep">下一步</button>
        </div>
        <div class="title">创建新记录</div>
        <div class="step1" v-show="step==1">
            <el-form ref="basicInfo" :model="basicInfo" :rules="rules" label-width="7em">
                <el-form-item label="名称" prop="title">
                    <el-input v-model="basicInfo.title" clearable style="width:200px; margin-left:1em">
                    </el-input>
                </el-form-item>
                <el-form-item label="导演" prop="director">
                    <el-input v-model="basicInfo.director" clearable style="width:200px; margin-left:1em"></el-input>
                </el-form-item>
                <el-form-item label="观影时间" prop="date">
                    <el-date-picker style="margin-left:1em" v-model="basicInfo.date" type="date" placeholder="选择日期"
                        format="yyyy 年 MM 月 dd 日" value-format="yyyy-MM-dd">
                    </el-date-picker>
                </el-form-item>
                <el-form-item label="添加标签">
                    <AddTags v-on:ch_tag="ch_tag" />
                </el-form-item>
            </el-form>
        </div>

        <div class="step2" style="width:70%; margin:auto;padding-bottom:2em" v-show="step==2">
            <div class="info">
                <i class="el-icon-reading icon"></i>
                <div class="main_info">
                    <div>{{basicInfo.title}}</div>
                    <div><span>导演：</span>{{basicInfo.director}}</div>
                </div>
                <div class="casts" v-show="basicInfo.casts[0]!==''">演员：<span v-for="(cast,i) in basicInfo.casts"
                        :key="i">{{cast}}</span></div>
                <div class="status_info">
                    <div><span>观影时间：</span>{{basicInfo.date}}</div>
                    <div>
                        <span>标签：</span>
                        <div class="tag" v-for="(item,i) in basicInfo.tag" :key="i" effect="plain">#{{item}}</div>
                    </div>
                </div>
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
        name: 'addWatch',
        components: {
            AddTags,
            tinymce
        },
        data() {
            return {
                type: 1,
                basicInfo: {
                    title: '',
                    director: '',
                    date: '',
                    casts: ['演员1'],
                    tag: []
                },
                rules: {
                    title: [{
                        required: true,
                        message: '请输入电影名',
                        trigger: 'change'
                    }],
                    director: [{
                        required: true,
                        message: '请输入导演',
                        trigger: 'change'
                    }],
                    date: [{
                        required: true,
                        message: '请选择时间',
                        trigger: 'change'
                    }],
                },
                exit: '',
                step: 1,
                step1: false,
                msg: 'use tinymce',
                disabled: true,
            }
        },
        methods: {
            //step1
            addCast() {
                if (this.basicInfo.casts[0] !== '') {
                    this.basicInfo.casts.push();
                }
            },
            ch_tag(tags) {
                let ch_tags = []
                tags.forEach(function (val, i) {
                    ch_tags[i] = val;
                });
                this.basicInfo.tag = ch_tags;
            },
            nextStep() {
                if (this.submit()!=false) {
                    this.step++
                    this.disabled = false;
                }
                if (this.step > 2) {
                    this.$router.push('/record')
                }
            },
            submit() {
                return this.$refs['basicInfo'].validate((valid) => {
                    if (valid) {
                        console.log(this.basicInfo)
                        return true
                    } else {
                        return false
                    }
                })
            },
            priStep() {
                if (this.step > 1) {
                    this.step--
                }
                if (this.step == 1) {
                    this.disabled = true;
                }
            }
            //step2

        },
        mounted() {},
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