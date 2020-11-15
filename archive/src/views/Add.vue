<template>
    <div class="add">
        <div class="title">
            添加新记录
        </div>
        <div class="recordinfo">
            <div style="margin-bottom:1em;">
                <el-radio-group v-model="radio" @change="radioChange" v-show="step1">
                    <el-radio :label="1">阅读记录</el-radio>
                    <el-radio :label="2">观影记录</el-radio>
                </el-radio-group>
            </div>
            <AddRead v-if="radio==1" :step="1"/>
            <AddWatch v-else />
        </div>
    </div>
</template>

<script>
    // @ is an alias to /src
    import AddRead from '@/components/addRead.vue'
    import AddWatch from '@/components/addWatch.vue'

    export default {
        name: 'Add',
        components: {
            AddRead,
            AddWatch
        },
        data() {
            return {
                radio: 1,
            }
        },
        methods: {
            radioChange(val) {
                this.radio = val;
            },
        },
    }
</script>
<style scoped>
    .steps {
        margin: 5em 10em;
    }

    .title {
        font-size: 1.5em;
        margin: 1em 2em;
        padding: 0.2em 0.51em;
        border-bottom: 1px solid;
        border-color: #888;
        color: #44a448;
    }

    .recordinfo {
        margin: auto;
        width: fit-content;

    }


</style>