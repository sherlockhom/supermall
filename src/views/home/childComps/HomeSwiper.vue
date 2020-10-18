<template>
    <div>
        <Swiper>
            <SwiperItem v-for="(item,index) in banners" :key="index">
                <a :href="item.link">
                    <img :src="item.image" alt="">
                </a>
            </SwiperItem>
        </Swiper>
    </div>
</template>

<script>
    import {Swiper,SwiperItem} from 'components/common/swiper'
    export default{
        name:'HomeSwiper',
        props:{
            banners:Array,
            default(){
                return[]
            }
        },
        components:{
            Swiper,
            SwiperItem
        }
    }
</script>

<style>
</style>
