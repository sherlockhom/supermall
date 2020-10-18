<template>
	<div class="wrapper">
        <ul class="content">
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
            <li>1</li>
        </ul>

    </div>
</template>

<script>
    import BScroll from 'better-scroll'
	export default{
		name:'Category',
        data(){
            return{
                scroll:null
            }
        },
        mounted() {
            this.scroll = BScroll(document.querySelector('.wrapper'),{
                // probeType表示侦测
                // 0,1都表示不侦测实时的位置
                // 2:在手指滚动时侦测,离开时不进行侦测
                // 3:只要发生滚动,都进行侦测
                probeType:2,
                // 设置上拉加载更多的功能
                pullUpLoad:true
            })
            // this.scroll.on('scroll',position => {
            //     console.log(position)
            // })
            // this.scroll.on('pullingUp',() => {
            //     console.log('上拉加载更多')
            //     this.scroll.finishiPullUp()
            // })

        },
        methods:{
            back(){
                this.scroll.scrollTo(0,0)
            }
        }

	}
</script>

<style scoped>
    .wrapper{
        height: 141px;
        background-color: red;
        overflow: hidden;
        /* overflow-y: scroll; */
    }
</style>
