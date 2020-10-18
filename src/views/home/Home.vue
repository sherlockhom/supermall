<template>
    <div id="home">
        <NavBar class='home-nav'>
            <template v-slot:center>购物车</template>
        </NavBar>
        <Scroll class="wrapper"  
                ref="scroll" 
                :probeType="3" 
                @scroll="contentScroll" 
                @loadMore="loadMore" 
                :pullUpLoad="true">
            <div>
                <HomeSwiper :banners="banners"></HomeSwiper>
                <RecommendView :recommends='recommends'></RecommendView>
                <FeatureView></FeatureView>
                <TabControl :titles="['流行','新款','精选']" class="tab-control" @tabclick="tabclick"></TabControl>
                <GoodList :goods="showGoods"></GoodList>
            </div>

        </Scroll>
        <BackTop @click.native="backClick" class="backTop" v-show="isShow"></BackTop>
    </div>
</template>

<script>
    import HomeSwiper from './childComps/HomeSwiper.vue'
    import RecommendView from './childComps/RecommendView.vue'
    import FeatureView from './childComps/FeatureView.vue'

    import NavBar from 'components/common/navbar/NavBar.vue'
    import TabControl from 'components/content/tabControl/TabControl.vue'
    import Scroll from 'components/common/scroll/Scroll.vue'
    import BackTop from 'components/content/backTop/BackTop.vue'
    import GoodList from 'components/content/goods/GoodsList.vue'


    export default {
        name: 'Home',
        data() {
            return {
                banners: [],
                recommends: [],
                goods: {
                    'pop': {
                        page: 0,
                        list: []
                    },
                    'new': {
                        page: 0,
                        list: []
                    },
                    'sell': {
                        page: 0,
                        list: []
                    }
                },
                currentType: 'pop',
                isShow:false
            }
        },
        components: {
            NavBar,
            HomeSwiper,
            RecommendView,
            FeatureView,
            TabControl,
            GoodList,
            Scroll,
            BackTop
        },
        created() {
            this.init();
            this.getHomeGoods('pop');
            this.getHomeGoods('new');
            this.getHomeGoods('sell');

            // 监听items图片加载完成
            this.$bus.$on('imageLoad', () => {
                this.$refs.scroll.refresh()
            })
        },
        mounted() {
            this.scroll
        },
        computed: {
            showGoods() {
                return this.goods[this.currentType].list
            }
        },
        methods: {
            // 网络请求
            init() {
                this.axios.get('http://123.207.32.32:8000/home/multidata').then(response => {
                    let res = response.data;
                    this.banners = res.data.banner.list;
                    this.recommends = res.data.recommend.list;
                    // console.log(res)
                })
            },
            getHomeGoods(type) {
                let page = this.goods[type].page + 1;
                this.axios.get('http://152.136.185.210:8000/api/w6/home/data', {
                    params: {
                        type,
                        page
                    }
                }).then(res => {
                    // console.log(res.data.data.list)
                    this.goods[type].list.push(...res.data.data.list);
                    // this.goods[type].page+=1;
                })

            },
            // 事件监听
            tabclick(index) {
                switch (index) {
                    case 0:
                        this.currentType = 'pop';
                        break;
                    case 1:
                        this.currentType = 'new';
                        break;
                    case 2:
                        this.currentType = 'sell';
                        break;
                }
            },
            backClick() {
                this.$refs.scroll.scrollTo(0,0)
            },
            contentScroll(position){
                this.isShow = -position.y > 1000;
            },
            loadMore(){
                this.getHomeGoods(this.currentType)
                this.$refs.scroll.finishPullUp()
            }
        }
    }
</script>

<style scoped>
    #home {
        /* position: relative; */
        /* padding-top: 44px; */
        height: 100vh;
    }

    .home-nav {
        background-color: var(--color-tint);
        color: #fff;
        position: fixed;
        right: 0;
        left: 0;
        top: 0;
        /* 设置堆叠顺序，使其在最顶层显示 */
        z-index: 9;
    }

    .tab-control {
        position: sticky;

        top: 44px;
        z-index: 9;
    }

    .wrapper {
        overflow: hidden;
        position: absolute;
        top: 44px;
        bottom: 49px;
        left: 0;
        right: 0;
    }
</style>
