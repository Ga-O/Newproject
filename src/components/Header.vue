<template>
    <div>
        <a href="javascript:;" class="logo-link">
            <img src="../../public/img/logo_white.png" alt="图片已丢失">
        </a>
        <nav>
            <ul class="header-list">
                <li><a href="javascript:;">最新活动</a></li>
                <li @mouseenter="getlist" @mouseleave="getlist" class="nav1">
                    <a href="javascript:;">产品</a>
                    <div class="sub-nav products-nav double-col" v-show="getshow">
                        <div class="nav-group">
                            <div class="nav-type">
                                <h6 :class="{'all-product':true,'current':-1===cur}" @mouseenter="addcur(-1)">全部产品</h6>
                                <h6 v-for="(item,i) in product" :key="item.id" @mouseenter="addcur(i)" :class="{current:i===cur}">{{item.pname}}</h6>
                            </div>
                            <ul class="nav-content">
                                <li data-isdouble  class="all-products-nav">
                                    <ul>
                                        <li class="lineItems items-0">
                                            <ul>
                                                <li class="product-type product-index-0">
                                                    <h5 class="type-title">计算机与网络</h5>
                                                    <ul v-if="product[0]">
                                                        <li class="product-item" v-for="item in product[0].child" :key="item.iid">
                                                            <a href="javascript:;">
                                                                <h5>{{item.iname}}</h5>
                                                            </a>
                                                        </li>
                                                    </ul>
                                                </li>
                                                <li class="product-type product-index-1">
                                                    <h5 class="type-title">数字营销云</h5>
                                                    <ul v-if="product[5]">
                                                        <li class="product-item" v-for="item in product[5].child" :key="item.iid">
                                                            <a href="javascript:;"><h5>{{item.iname}}</h5></a>
                                                        </li>
                                                    </ul>
                                                </li>
                                            </ul>
                                        </li>
                                    </ul>
                                </li>
                                <li data-isdouble class=""></li>
                            </ul>
                        </div>
                    </div>
                </li>
                <li @mouseenter="getlist" @mouseleave="hidelist">
                    <a href="javascript:;">解决方案</a>
                    <div class="sub-nav">
                        <div class="nav-group">
                            <div class="nav-type">
                                <h3></h3>
                            </div>
                            <ul class="nav-content">
                                <li></li>
                            </ul>
                        </div>
                    </div>
                </li>
                <li @mouseenter="getlist" @mouseleave="hidelist">
                    <a href="javascript:;">云市场</a>
                </li>
                <li @mouseenter="getlist" @mouseleave="hidelist">
                    <a href="javascript:;">合作与生态</a>
                </li>
                <li @mouseenter="getlist" @mouseleave="hidelist">
                    <a href="javascript:;">帮助与支持</a>
                </li>
            </ul>
        </nav>

    </div>
</template>
<script>
    export default{
        created(){

            this.getinfo()
        },
        data() {
            return {
                getshow:false,
                product:[
                ],
                cur:"",
                isTrue:true,
            };
        },
        methods: {
            getlist(){
                this.getshow=true;
            },
            hidelist(){
                this.getshow=false;
            },
            getinfo(){
                this.$http.get("./../../static/data.json").then(result=>{
                    this.product=result.data.product;
                    console.log(this.product);


                })
            },
            addcur(i){
                this.cur=i;
            },
            recur(){
                this.cur="";
            },
            addcurrent(){
                this.isTrue=true;
            },
            recurrent(){
                this.isTrue=false;
            }
        }
    }
</script>
<style>
    .logo-link{
       float:left;
       margin-top:16px;
    }
    .logo-link>img{
        width:88px;
    }
    nav{
        padding-left:100px;
    }
    .header-list{
        height:60px;
        margin:0;
    }
    .header-list>li{
        float:left;
        height:100%;
        line-height: 60px;
    }
    .header-list>li:hover:after{
        content: '';
	    display: block;
	    margin-top: -3px;
	    margin-left: -10px;
	    padding: 0 10px;
	    width: 100%;
	    height: 3px;
	    background-image: linear-gradient(to left, #00A1FF, #0B62FF);
        background-repeat: repeat;

    }
    .header-list>li>a{
        display:inline-block;
        height:100%;
        color:#fff;
        font-size:14px;
    }
    .header-list>li>a:hover{
        color:#108CEE;
    }
    .header-list>li{
        margin-left:25px;
    }
    .nav1>a{
        width:50px;
    }
    .header-list .nav1{
        margin-left: 10px;
        margin-right: -10px;
    }
    .sub-nav{
        position:absolute;
        background:#101019;
        height:auto;
    }
    .products-nav{
        width:663px;
        top:60px;
        margin-left:-110px;
    }
    .products-nav.double-col{
        width:1160px;
    }
    .sub-nav>.nav-group{
        position:relative;
        min-height:495px;
        overflow:hidden;
    }
    .nav-type{
        height:100%;
        position:absolute;
        left:0;
        width:245px;
        border-right:1px solid #35353D;
        padding-top:15px;
        overflow: hidden;
    }
    .nav-type h6{
        text-align:left;
        position:relative;
        color:#999;
        font-weight: normal;
        font-size:14px;
        width:100%;
        height:40px;
        line-height: 40px;
        display:block;
        cursor: pointer;
        padding-left:45px;
        margin:0;

    }
    .nav-group .nav-type h6.all-product{
        background:#101019 url("../../public/img/header/all.png") 200px -20px no-repeat;
    }
    .nav-type h6.all-product.current{
        background-color: #1B1B25;
        background-position: 200px 14px;
    }
    .nav-type h6.current {
        background: #1B1B25 url("../../public/img/header/icon1.png") 200px -117px no-repeat;
        color: #0b83e1;
        padding-left: 60px;
        transition: padding-left 0.3s cubic-bezier(0, 1.13, 1, 1);
    }
    .nav-content>.all-products-nav{
        width:887px;

    }

    .sub-nav .nav-group .nav-content{
        overflow: hidden;
    }
    .products-nav .nav-group>ul{
        float: none;
        margin: 8px 0 8px 250px;
    }
    .nav-content>.all-products-nav .lineItems {
        width:140px;
        float:left;
        text-align:left;
        margin:0 20px;
    }
    .nav-content>.all-products-nav .lineItems .product-type li{
        height:30px;
        line-height:30px;
    }
    .products-nav ul h5.type-title{
        opacity: 0.4;
        height:50px;
        line-height: 50px;
    }
    .products-nav h5{
        font-weight: normal;
        opacity: .8;

    }

    .sub-nav li a{
        color:#fff;
        height:100%;
    }
    .product-type .product-item h5:hover{
        color:#0b83e1;
    }
</style>
