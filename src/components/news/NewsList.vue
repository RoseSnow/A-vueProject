<template>
    <div>
        <!-- 导航条[新闻分类] -->
        <!-- <div id="slider" class="mui-slider">
            <div id="sliderSegmentedControl" class="mui-scroll-wrapper mui-slider-indicator mui-segmented-control mui-segmented-control-inverted">
                <div class="mui-scroll">
                    <a class="mui-control-item mui-active" v-for="item in newslist" :key="item.docid">
                        {{ item[2].category }}
                    </a>
                </div>
            </div>

        </div> -->


        <ul class="mui-table-view">
            <li class="mui-table-view-cell mui-media" v-for="item in newslist" :key="item.uniquekey">
                <router-link :to="'/home/newsinfo/' + item.uniquekey">
                    <img class="mui-media-object mui-pull-left" :src="item.thumbnail_pic_s02">
                    <!-- 这里图片请求不过来未解决 :src="item.picInfo[0].url" -->
                    <div class="mui-media-body">
                        <h1>{{ item.title }}</h1>
                        <p class='mui-ellipsis'>
                            <span>发表时间：{{ item.date }}</span>
                            <span>发表机关：{{ item.author_name }}</span>
                        </p>
                    </div>
                </router-link>
            </li>
        </ul>
    </div>
</template>

<script>
// import mui from "../../../static/mui/js/mui.min.js";
import { Toast } from "mint-ui";
export default{
    data(){
        return{
            newslist:[]
        }
    },
    created(){
        this.getNewslist();
    },
    // mounted(){
    //     mui('.mui-scroll-wrapper').scroll({
    //         deceleration: 0.0005 // flick 减速系数 系数越大 滚动速度越慢 滚动距离越小 默认值0.0006
    //     })
    // },
    methods:{
        getNewslist(){
            // 获取新闻列表 api https://www.apiopen.top/journalismApi 可用
            this.$axios.get('/newsapi/index?key=030199af1649b49b8da6bf2ca54d968e').then(res=>{
                // console.log(res.data.reason);
                // console.log(res.data.result);
                // console.log(res.data.result.data);
                // console.log(res.data.result.stat);
                if(res.data.reason === "成功的返回"){
                    this.newslist = res.data.result.data;
                }else{
                    Toast('获取失败！')
                }

            })
        }
        // getNewslist(){
        //     this.$axios.get("https://www.apiopen.top/journalismApi").then(res => {
        //         if(res.data.code === 200){
        //             this.newslist = res.data.data;
        //         }
        //     })
        // }
    }
}
</script>

<style lang="scss" scoped>
.mui-table-view{
    li{
        h1{
            font-size: 14px;
            overflow: hidden;
            white-space: nowrap;
            text-overflow : ellipsis;
        }
        .mui-ellipsis{
            font-size: 12px;
            color: #226aff;
            display: flex;
            justify-content: space-between;
        }

        .mui-media-object{
            width: 100%;
        }
    }
}
</style>
