<template>
    <div class="addTags">

        <div style="display:flex">
            <div style="margin-right:1em">添加标签</div>

            <div>
                <div class="choosed_tags">
                    <el-tag v-for="(item,i) in choosed_tags" :key="i" closable :disable-transitions="false"
                        @close="deleteTag(i)">{{item}}
                    </el-tag>
                </div>
                <div class="tags">
                    <el-tag effect="plain" v-for="(item,i) in tags" :key="i" @click="chooseTag(item)">+ {{item}}
                    </el-tag>
                </div>
                <div>
                    <el-input placeholder="创建新标签，多个标签用分号分隔" size="medium" v-model="tag" maxlength="20"
                        @keyup.enter.native="addTag" style="width:20em " @blur="addTag">
                    </el-input>
                </div>
            </div>

        </div>

    </div>
</template>
<script>
    export default {
        data() {
            return {
                tag: '',
                tags: ['tag1', 'tag2', 'tag3'],
                tagAlert: 0,
                choosed_tags: [],
            }
        },
        props:{
            exit_tags:Array
        },
        methods: {
            addTag() {
                let tag = this.tag;
                if (tag) {
                    let new_tags = tag.split(/;|；/);
                    //去重
                    //tag1;tag1;tag2;tag1
                    for (let i = 0; i < new_tags.length; i++) {
                        for (let j = i + 1; j < new_tags.length; j++) {
                            let bool = new_tags.indexOf(new_tags[i], j)
                            if (bool != -1) {
                                new_tags.splice(bool, 1)
                            }
                        }
                    }
                    //添加
                    //tag1;tag2;tag4;tag1
                    new_tags.forEach(element => {
                        if (this.choosed_tags.indexOf(element) == -1) {
                            this.choosed_tags.push(element)
                        }
                    });

                }
                this.$emit('tags', this.choosed_tags);
                this.tag = ''
            },
            chooseTag(tag) {
                if (this.choosed_tags.indexOf(tag) == -1) {
                    this.choosed_tags.push(tag);
                    this.$emit('tags', this.choosed_tags);
                }

            },
            deleteTag(index) {
                this.choosed_tags.splice(index, 1);
                this.$emit('tags', this.choosed_tags);

            }
        },
        watch: {
            exit_tags:function(){
                this.choosed_tags=this.exit_tags;
            }
        },
    }
</script>
<style scoped>
    .tags>.el-tag,
    .choosed_tags>.el-tag {
        margin-right: 1em;
        margin-bottom: 1em;

    }
</style>