<template>
    <div>
        <div class="nav">
            <el-breadcrumb>
                <el-breadcrumb-item :to="{ path: '/' }">{{type=='read' ? '阅读':'观影'}}记录</el-breadcrumb-item>
                <el-breadcrumb-item :to="{paht:'/2020'}">2020</el-breadcrumb-item>
                <el-breadcrumb-item :to="{paht:'/2020'}">10</el-breadcrumb-item>
                <!-- <el-breadcrumb-item :to="{paht:'/2020'}">title</el-breadcrumb-item> -->
            </el-breadcrumb>
        </div>
        <div class="record">
            <div class="main">
                <h1 class="title"><i class="el-icon-film icon"></i> Title</h1>
                <div class="main_info">
                    <img src="../assets/avatar.png" alt="avatar" class="avatar">
                    <a href="#">welsea</a>
                    <span>2020-10-22</span>
                </div>
                <div>
                    <div v-for="(item,i) in content" :key="i">{{item}}</div>
                </div>
            </div>
            <div class="side">
                <div class="info">
                    <!-- <div class="main_info"> -->
                    <div><span>电影：</span>{{basicInfo.name}}</div>
                    <div><span>导演：</span>{{basicInfo.director}}</div>
                    <!-- </div> -->
                    <div class="casts" v-show="basicInfo.casts[0]!==''"><span>演员：</span>
                        <div v-for="(cast,i) in basicInfo.casts" :key="i" class="cast">{{cast}},</div>
                    </div>
                    <!-- <div class="status_info"> -->
                    <div><span>观影时间：</span>{{basicInfo.date}}</div>
                    <div v-show="basicInfo.tag.length!==0">
                        <span>标签：</span>
                        <div class="tag" v-for="(item,i) in basicInfo.tag" :key="i" effect="plain">#{{item}}</div>
                    </div>
                    <!-- </div> -->
                </div>
                <!-- 读书记录显示 -->
                <div class="other" v-show="type=='read'">
                    <div>《厌女》的其他记录：</div>
                    <a href="#" v-for="i in 5" :key="i">其他记录标题{{i}}</a>
                    <div>>>查看全部</div>
                </div>
            </div>
        </div>
    </div>

</template>
<script>
    // import UserInfo from '@/components/UserInfo.vue'

    // import txt from '../../static/fill.txt'
    export default {
        component: {
            // UserInfo
        },
        data() {
            return {
                basicInfo: {
                    name: 'Blade runner 2049',
                    director: 'Ledly Samul',
                    date: '2020-10-12',
                    casts: ['Ryan Gosling', 'Aia Lysell'],
                    tag: ['sic', 'rg']
                },
                title: '银翼杀手影评',
                content: [],
                type:''
            }
        },
        methods: {
            fillContent() {
                this.content = [
                    "从小到大，总觉得自己与同龄人有些格格不入。特别是那些过于纤细娇媚的女生，是自卑也好是觉得她们做作也好，与这些女人味十足的女生在一起总觉得不太习惯。每当女生们开始聊过于女生的话题时，比如化妆品，包包，首饰，各种牌子等等，当她们开始互相比较吹捧时，我觉得自己就像是个局外人，只觉无聊尴尬甚至发慌，只想从现场快速离开。而与男生相处，稍微自在一些，但也觉得自己其实并不在那个群体里。当他们共同开起关于女生的玩笑，我就会觉得格外地孤立。只有当和我差不多类型的女生相处时，才觉得不那么孤独。这种深刻的异类感直到读了日本社会学家上野千鹤子所写的《厌女》之后才恍然大悟，原来是这样啊。",
                    "厌女症，简单来说，就是女性的自我厌恶，以及男性对女性的蔑视。不要觉得这只是少数人才会有的毛病。可以说在性别二元制的秩序里，处在核心位置的就是厌女症。每个人都是厌女症患者，只是大家没有意识到罢了。像防火防盗防闺蜜，恐同，荡妇歧视，剩女，A男配B女等等概念大家大概并不陌生，其实这些都是厌女症的表现啊。",
                    "就像书中译者后话所说“兄弟如手足，女人如衣裳”，这句简单的中国俗语一语道破厌女症的根源。兄弟之情才是男人世界的根基。我一直特别羡慕男人的世界，男人的友谊。总觉得男人之间的友请来得更加纯粹和深厚，不像女人薄得就和火腿片一样的友情，特别脆弱。男人之间这种强有力的手足之情有一个专有名词叫做男性同性社会性欲望（homosocial），由美国学者塞吉维克所提出。它指的是男人之间不带性的关系，即男人之间相互认同的欲望。区别于男性同性恋（malehomosexual）。男人之所以成为男人，不是被女人选上而成为男人，而是在男人集团中被承认为正式成员。男人的价值是在男人的世界里确定的。要成为男人，要被男人集团承认，必须确认自己是性的主体（即主动插入而非被插入的一方）。而确认男人这一主体性，就需要排除非男人，即将女人他者化，客体化并加以蔑视，这便是厌女症的来源。同时为了要维系这种男人集团的同质性，必须排除同性恋，即“像女人的男人”。 因为同性恋很有可能让男人成为被插入的一方，即性的客体，从而被女性化。这就是恐同的由来。“因此男人的同性社会性欲望的纽带，也就是互相认可的性的主体者之间的纽带。这种纽带建立在厌女症的基础上，由同性恋憎恶来维系”。说白了就是“男人之间的团结，是通过将没能成为男人的人和女人排除在外并加以歧视而成立的。”",
                ]
            }
        },
        created() {
            this.fillContent();
            this.type=this.$route.query.type;
        },
    }
</script>
<style scoped>
    .nav {
        padding: 1em 2em;
        background-color: #0080001a;
    }

    .record {
        width: 70%;
        margin: auto;
        display: flex;
        align-items: flex-start;
        justify-content: space-between;
        padding-bottom: 5em;
    }

    .record>div:first-child {
        width: 70%
    }

    .side {
        margin-top: 5em;
        font-size: 0.8em;
        width: 20%
    }
    .other{
        margin-top: 4em;
    }
    .other>a {
        display: block;
        /* padding-left: 2em; */
        color: #008000ad;
        width: 100%;
        text-decoration: none;
        border-bottom: 1px dotted;
        padding: 0.5em 2em;
        border-color: #ddd;
        font-size: 0.8em;
    }

    .other>div:first-child{
        color:green;
    }
    .other>div:last-child{
        color:#888;
        font-size: 0.8em;
        text-align: right;
    }
    .title {
        position: relative;
        right: 1.5em;
    }

    .info span {
        color: #00800061;
        ;
    }

    .info {
        color: green;
    }

    .info>div {
        margin-bottom: 1em;
    }

    .main_info {
        display: flex;
        flex-direction: row;
        align-items: center;
        font-size: 0.9em;
        color: #888;
        margin-bottom: 1.5em;
    }

    .main_info>a {
        margin: 0 1em 0 0.5em;
    }

    .avatar {
        width: 2em;
    }

    .avatar> {
        margin-left: 1em;
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

    .cast {
        display: inline-block;
        font-size: 0.9em;
        margin-right: 0.2em
    }
</style>