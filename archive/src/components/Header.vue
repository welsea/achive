<template>
    <div>
        <el-container>
            <el-header>
                <el-menu :default-active="this.$route.path" router mode="horizontal" background-color="#f6f6f6"
                    active-text-color="#ffd04b">
                    <el-menu-item v-for="(item,i) in navList" :key="i" :index="item.name">
                        {{ item.navItem}}
                    </el-menu-item>
                </el-menu>
            </el-header>
            <el-main>
                <el-row :gutter="24">
                    <el-col :span="18" :offset="3">
                        <router-view></router-view>
                    </el-col>
                </el-row>
            </el-main>
            <el-footer id="footer">
                <Footer></Footer>
            </el-footer>
        </el-container>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                navList: [{
                        name: '/',
                        navItem: "首页"
                    },
                    {
                        name: '/home',
                        navItem: "home"
                    },


                ],
                circleUrl: '.../public/icon.jpg',
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