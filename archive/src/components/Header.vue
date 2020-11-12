<template>
    <div>

        <el-menu :default-active="this.$route.path" router mode="horizontal">
            <el-menu-item v-for="(item,i) in navList" :key="i" :index="item.name">
                {{ item.navItem}}
            </el-menu-item>
        </el-menu>

    </div>
</template>

<script>
    export default {
        data() {
            return {
                navList: [{
                        name: '/home',
                        navItem: "home"
                    },
                    {
                        name: '/about',
                        navItem: "about"
                    },


                ],
                search_e: '',
                activeIndex: '1',
                activeIndex2: '1'
            }
        },
        method: {
            // handleSelect(key,keyPath){
            //     console.log(key,path)
            // }
        }


    }
</script>