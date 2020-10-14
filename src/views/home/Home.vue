<template>
	<div id="home">
        <NavBar class='home-nav'>
            <template v-slot:center>购物车</template>
        </NavBar>
    </div>
</template>

<script>
    import NavBar from 'components/common/navbar/NavBar.vue'
	export default{
		name:'Home',
        data(){
            return{
                result:null
            }
        },
        components:{
            NavBar
        },
        mounted(){
            this.init();
        },
        methods:{
            init(){
                this.axios.get('http://123.207.32.32:8000/home/multidata').then(res => {
                    this.
                    console.log(res)
                })
            }
        }
	}
</script>

<style>
    .home-nav{
        background-color: var(--color-tint);
        color: white;
    }
</style>
