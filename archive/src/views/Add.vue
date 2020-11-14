<template>
    <div class="add">
        <div class="title">
            添加新记录
        </div>
        <div class="recordinfo" v-show="setp1">
            <div style="margin-bottom:1em;">
                <el-radio-group v-model="radio" @change="radioChange">
                    <el-radio :label="1">阅读记录</el-radio>
                    <el-radio :label="2">观影记录</el-radio>
                </el-radio-group>
            </div>
            <AddRead v-if="radio==1" />
            <AddWatch v-else />
            <el-button primary @click="nextStep">Next</el-button>
        </div>
        <div v-show="step2">
            
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
                setp1:true,
                step2:false
            }
        },
        methods: {
            radioChange(val) {
                this.radio = val;
            },
            nextStep(){
                this.step1=false;
                this.step2=true;
            }
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