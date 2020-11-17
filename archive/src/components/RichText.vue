<template>
    <div class="tinymce">
        <Editor id="tinymce" v-model="value" :init="init">
        </Editor>
    </div>
</template>

<script>
    import tinymce from 'tinymce/tinymce' //tinymce默认hidden，不引入不显示
    import Editor from '@tinymce/tinymce-vue'
    import '../../static/tinymce/skins/ui/oxide/skin.css'
    import '../../static/tinymce/zh_CN.js'
    import 'tinymce/themes/silver'
    import 'tinymce/icons/default'

    // 编辑器插件plugins
    import 'tinymce/plugins/link' // 插入链接
    import 'tinymce/plugins/image' // 插入上传图片插件
    import 'tinymce/plugins/lists' // 列表插件
    import 'tinymce/plugins/wordcount' // 字数统计插件

    export default {
        components: {
            Editor
        },
        name: 'tinymce',
        data() {
            return {
                init: {
                    selector: "#tinymce", //tinymce的id
                    height:'500',
                    language_url: "../../static/tinymce/zh_CN.js",
                    language: "zh_CN",
                    skin: 'borderless',
                    skin_url: "../../static/tinymce/skins/ui/oxide", 
                    menubar:false,
                    plugins:'link lists image wordcount',
                    toolbar:'undo redo |  formatselect | bold italic | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | image | removeformat',
                    // image_title:true,
                    // file_picker_types: 'image',

                },
                value:''
            }
        },
        mounted() {
            tinymce.init({})
        },
        methods: {

        },
        watch: {

        }
    }
</script>
<style scoped>

</style>