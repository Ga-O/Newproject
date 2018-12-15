<template>
    <header>
        <Header></Header>
        <router-view></router-view>
    </header>
</template>
<script>
    import Header from '@/components/Header.vue'

    export default{
        data(){
            return{}
        },
        components: {
            Header
        }
    }
</script>
<style>
    header{
        min-width: 1280px;
        background:rgba(0,0,0,0.8);
        color:#fff;
        height:60px;
    }
    header>div{
        width:1180px;
        margin:0 auto;
        height:100%;
    }
    #header>div:after{
        content:"";
        display:block;
        clear:both;
    }
</style>