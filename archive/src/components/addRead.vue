<template>
    <div class="addRead">
        <div style="margin-bottom:1em;">
            <el-radio-group v-model="type" @change="typeChange">
                <el-radio :label="1">新建</el-radio>
                <el-radio :label="2">添加已有</el-radio>
            </el-radio-group>
        </div>
        <div class="new" v-if="type==1">
            <div>书名<el-input v-model="title" clearable style="width:200px; margin-left:1em"></el-input>
            </div>
            <div>作者<el-input v-model="author" clearable style="width:200px; margin-left:1em"></el-input>
            </div>
            <div>开始时间<el-date-picker style=" margin-left:1em" v-model="start" type="date" placeholder="选择日期">
                </el-date-picker>
            </div>
            <div>
                状态
                <el-radio-group v-model="status" @change="statusChange">
                    <el-radio :label="1" style=" margin-left:1em">已读完</el-radio>
                    <el-radio :label="2">未读完</el-radio>
                </el-radio-group>
            </div>
            <div>
                <AddTags />
            </div>
        </div>
        <div v-else></div>
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
                title: '',
                author: '',
                start: '',
                status: 1
            }
        },
        methods: {
            radioChange(val) {
                this.radio = val;
            },
            typeChange(val) {
                this.type = val;
            },
            statusChange(val) {
                this.status = val;
            }
        },
    }
</script>
<style scoped>
    .new>div {
        margin-bottom: 1em;
    }
</style>