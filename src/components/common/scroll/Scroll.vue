<template>
    <div  ref="wrapper">
            <slot></slot>
    </div>
</template>

<script >
    import BScroll from 'better-scroll'
    export default {
        name: 'Scroll',
        props: {
            probeType:{
                type:Number,
                default:0
            },
            pullUpLoad:{
                type:Boolean,
                default: false
            }
        },
        data() {
            return {
                scroll: null
            }
        },
        mounted() {
            this.scroll = new BScroll(this.$refs.wrapper, {
                // probeType表示侦测
                // 0,1都表示不侦测实时的位置
                // 2:在手指滚动时侦测,离开时不进行侦测
                // 3:只要发生滚动,都进行侦测
                probeType: this.probeType,
                // 设置上拉加载更多的功能，
                click:true,
                pullUpLoad: this.pullUpLoad
            })
            console.log(this.scroll)

            this.scroll.on('scroll',(position) => {
                this.$emit('scroll',position)
            })
            this.scroll.on('pullingUp',() => {
                console.log('上拉加载更多');
                this.$emit('loadMore')
                

            })
        },
        methods:{
            scrollTo(x,y,time=300){
                this.scroll.scrollTo(x,y,time)
            },
            refresh(){
                this.scroll.refresh()
            },
            finishPullUp(){
                this.scroll.finishPullUp();
            }
        }
    }
</script>

<style>

</style>
