<template>
  <div class='viewport'>
    <van-search
        v-model="value"
        shape="round"
        background="#63c9a4"
        left-icon
        right-icon="search"
        placeholder="请输入需要查找的内容"
        @search="onSearch"
    />
    <div class="viewport-main">
        <!-- 轮播图 [[ -->
        <van-swipe :autoplay="3000" indicator-color="#d7514a" class="swiperes">
            <van-swipe-item v-for="(image, index) in images" :key="index">
                <img :src="image"/>
                <div></div>
            </van-swipe-item>
        </van-swipe>
        <!-- 轮播图 ]] -->

        <!-- menu [[]] -->
        <van-grid :border="false" :column-num="5" class="menuList">
            <van-grid-item v-for="(menu, index) in menus" :key="index" @click="onClickMenu(index)">
                <van-image :src="menu.imgSrc"/>
                <div class="label-item" :class="current == index ? 'active' : ''" :style="{color: current == index ? fontColor : '#333'}">{{ menu.label }}</div>
            </van-grid-item>
        </van-grid>
        <!-- menu [[]] -->

        <!-- 猜你喜欢 [[ -->
        <div class="prefer">
            <div class="title clearfix">
                <span class="fl">猜你喜欢</span>
                <van-icon name="arrow" class="arrow-right fr"/>
            </div>
             <van-grid :border="false" :column-num="3" class="preferList">
                <van-grid-item v-for="(prefer, index) in preferes" :key="index">
                    <van-image :src="prefer.imgSrc"/>
                    <div class="label-item">{{ prefer.label }}</div>
                    <div class="second-label-item">{{ prefer.introduce }}</div>
                </van-grid-item>
            </van-grid>
        </div>
        <!-- 猜你喜欢 ]] -->

        <!-- 歌手信息--推荐 [[ -->
        <div class="prefer">
            <div class="title clearfix">
                <span class="fl">歌手信息-推荐</span>
                <van-icon name="arrow" class="arrow-right fr"/>
            </div>
             <van-grid :border="false" :column-num="4" class="singerList">
                <van-grid-item v-for="(singer, index) in singeres" :key="index" @click="showSingerDetail(index)">
                    <van-image :src="singer"/>
                </van-grid-item>
            </van-grid>
        </div>
        <!-- 歌手信息--推荐 ]] -->

        <!-- 圆角弹窗 [[ -->
        <van-popup v-model="showInfo" round closeable position="top" close-icon-position="bottom-right" :style="{height: '30%'}">
            <dl class="singerInformation">
                <dt>歌手基本信息</dt>
                <dd>中文名：{{ singerInformation[this.singerIndex].name }}</dd>
                <dd>英文名：{{ singerInformation[this.singerIndex].EnglishName }}</dd>
                <dd>生日：{{ singerInformation[this.singerIndex].birthday }}</dd>
                <dd>国籍：{{ singerInformation[this.singerIndex].country }}</dd>
            </dl>
        </van-popup>
        <!-- 圆角弹窗 ]] -->

        <!-- 下拉刷新 [[ -->
        <van-pull-refresh v-model="isLoading" @refresh="onRefresh"></van-pull-refresh>
        <!-- 下拉刷新 ]] -->
    </div>
  </div>
</template>

<script>
import { Toast } from 'vant';
export default {
  name: '',
  data(){
    return {
        value:"",
        activeNames:['1'],
        images:[
            '/static/images/banner.png',
            '/static/images/singer02.png',
            '/static/images/singer03.png'
        ],
        menus:[
            {imgSrc: '/static/images/icon_01.png', label:"短信"},
            {imgSrc: '/static/images/icon_02.png', label:"备忘录"},
            {imgSrc: '/static/images/icon_03.png', label:"标签"},
            {imgSrc: '/static/images/icon_04.png', label:"电话"},
            {imgSrc: '/static/images/icon_05.png', label:"视频"}
        ],
        preferes:[
            {imgSrc: '/static/images/singer01.png', label:"YOU DESER", introduce:"LEDR"},
            {imgSrc: '/static/images/singer02.png', label:"YOU DESER", introduce:"LEDR"},
            {imgSrc: '/static/images/singer03.png', label:"YOU DESER", introduce:"LEDR"}
        ],
        singeres:[
            '/static/images/people01.png',
            '/static/images/people02.png',
            '/static/images/people03.png',
            '/static/images/people04.png',
        ],
        current: null,//当前menu下标
        fontColor: null,
        showInfo: false,//歌手信息model
        isLoading: false,
        singerInformation:[
            {
                name:"周杰伦",
                EnglishName:"Jay Chou",
                birthday:"1979年1月18日",
                country:"中国台湾",
            },
            {
                name:"陈奕迅",
                EnglishName:"Eason Chan",
                birthday:"1974年7月27日",
                country:"中国香港",
            },
            {
                name:"黄家驹",
                EnglishName:"Wong Ka Kui",
                birthday:"1962年6月10日",
                country:"中国香港",
            },
            {
                name:"莫文蔚",
                EnglishName:"Karen Joy Morris",
                birthday:"1970年6月2日",
                country:"英国",
            }
        ],
        singerIndex: 0
    }
  },
  components: {},
  created(){},
  mounted(){},
  methods: {
    //搜索
    onSearch(val){
        Toast.loading({
            message:"加载中...",
            forbidClick: true
        })
    },
    //点击menu
    onClickMenu(index){
        this.current = index;
        switch(index){
            case 0:
                this.fontColor = '#ee736f';
                break;
            case 1:
                this.fontColor = '#f3ae53';
                break;
            case 2:
                this.fontColor = '#63c9a4';
                break;
            case 3:
                this.fontColor = '#48a7f8';
                break;
            case 4:
                this.fontColor = '#8872e2';
                break;
        }

    },
    //歌手详情
    showSingerDetail(index){
        this.showInfo = true;
        console.log(index)
        this.singerIndex = index;
    },
    //下拉刷新
    onRefresh(){
        console.log('下拉刷新~')
        setTimeout(()=>{
            Toast('刷新成功');
            this.isLoading = false;
        })
    }
  }
}
</script>
<style lang="less" scoped>
.color-grey{
    color: #999;
    font-size: 32px;
    line-height: 50px;
}
.viewport{
    width: 100vw;
    .viewport-main{
        margin: 0 40px;

        .swiperes{
            margin-top: 38px;
            
            img{
                width: 100%;
                height: 272px;
            }
        }

        .menuList{
            border-bottom: 2px solid #eeeeee;
            img{
                width: 80px;
                height: 80px;
            }
            .label-item{
                font-size: 24px;
                color: #333;
                margin-top: 24px;
            }
             .label-item.active{
                font-weight: bold;
             }  
        }

        .preferList{
            .van-image{
                width: 180px;
                height: 180px;
            }
            .label-item{
                width: 100%;
                text-align: left;
                font-size: 24px;
                color: #333;
                margin: 20px 0 10px 0;
            }
            .second-label-item{
                width: 100%;
                text-align: left;
                font-size: 20px;
                color: #999;
            }
        }
    }
}
.prefer{
    .title{
        font-size: 30px;
        margin: 40px 0 10px 0;

        .arrow-right{
            color: #666666;
        }
    }
}
dl.singerInformation{
    padding: 0 40px;
    dt{
        border-left: 12px solid #3399ff;
        line-height: 36px;
        text-indent: 20px;
        font-size: 34px;
        margin-bottom: 40px;
    }
    dd{
        margin: 25px 0;
        font-size: 26px;
    }
}
</style>
