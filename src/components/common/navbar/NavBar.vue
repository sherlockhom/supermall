<template>
    <div class="nav-bar">
        <div class="left"><slot name="left"></slot></div>
        <div class="center"><slot name="center"></slot></div>
        <div class="right"><slot name="right"></slot></div>
    </div>
</template>

<script>
    export default{
        name:'NavBar'
    }
</script>

<style>
    .nav-bar{
        display: flex;
        height: 44px;
        line-height: 44px;
        text-align: center;
        /* box-shadow: 0px 0px 10px 2px red ; */
    }
    .left,.right{
        width:60px;
        /* background-color: red; */
    }
    .center{
        flex:1;
        /* background-color: green; */
        font-size: 16px;
    }
</style>
