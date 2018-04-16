<template>
	<div class="pager">
		<div class='head' id='head'>
			<div class='top-div' id='top-div'>
				<div class='center-title'>{{headData.title}}</div>
				<img :src="headData.favorite" class="favorite">
			</div>
			<div class='bottom-div'>
				<div class="left-logo">
					<img :src="headData.left_logo">
				</div>
				<div class="contain-right">
					起送￥{{headData.sendFee}} | 配送￥ {{headData.packingFee}} | 送达{{headData.forwardTime}}分钟
				</div>
			</div>
			<div class='common-nav-menu'>
				<div class="center-title">
					<a class='active'>商品</a>
					<a>评价</a>
					<a>商家</a>
				</div>		
			</div>
		</div>

	    <!-- <component :is='component' id='content-component' @changenums="changenums"></component> -->
	    <div class='cart-content'  v-show='cartList&&nums>0'>
			<ul>
				<li v-for="(item,index) in cartData" v-if='item.num>0'>
					<div class="cl-r1">{{item.name}}</div>
					<div class="cl-r3">￥{{item.price}}</div>
					<div class="cl-r2">
						<i @click='plus(item,index)'>-</i>
				    		<span style="padding:0 5px;">{{item.num}}</span>
				    	<i @click='item.num=item.num+1;nums=nums+1;'>+</i>
			    	</div>
				</li>
			</ul>
	    </div>
	    <div class='cart-dark' v-show='cartList&&nums>0' @click="cartList=false"></div>
        <Goods @changenums="changenums"></Goods>

        
    
		<div class='footer'>
		   	<div class='shop' @click='watchCart'>
		   		<div class='cart-count' v-show='nums>0'>{{nums}}</div>
		   		<img src='../assets/shop.png'>
		   	</div>
		   	<span class='total-money'>共￥{{total}}元</span>
		   	<span class='choose-ok' @click='Payment'>选好了</span>
		</div>

		
		<!-- <div class='mul-mark'></div> -->

	</div>
</template>

<script>
import Goods from '../components/Goods'
import axios from 'axios'
export default {
	data () {
		return {
			headData:{},
			// component:"Goods",
			nums:0,
			cartList:false,
			cartData:[],
			total:0

		}
	},
	watch:{
		cartData:function(e){
			let m=0
			for (var i=0;i<e.length;i++){
				m=m+e[i].price*e[i].num
			}
			this.total=m
		}
	},
	components:{
		"Goods":Goods
    },
	mounted(){
	    axios.get('/api/head').then((res)=>{
	        this.headData=res.data
		})
	},
	methods:{
		plus(item,index){
			item.num=item.num-1;
			this.nums=this.nums-1;
			this.cartData=this.cartData.splice(index,1)
		},
		changenums(obj){
			this.nums=obj.numtotal
			this.cartData=obj.cartData;

		},
		watchCart(){
			this.cartList=!this.cartList
		},
		Payment(){
			if(this.total>0)
				alert("请支付"+this.total+"元")
			else
				alert("请选择商品")
		}
	}
}
</script>
<style>
	body{
		width:100%;
		height:100%;
		margin:0;
		padding:0;
		font-size: 14px;
	    font-family: Helvetica;
	    -webkit-font-smoothing: antialiased;
	}
	.head{
		background: #ed813f;
		position: fixed;
		top:0;
		width:100%;
		font-size: 100%;
		z-index: 3;
	}
	.center-title{
		text-align: center;
		font-size: .747rem;
		padding-top: .597rem;
		color:#ffffff;
		width:70%;
		margin-left: 15%;
		display: inline-block;	
	}
	.head .favorite{
		display: inline-block;
		width:.896rem;
		height:.811rem;
		margin-top: .5rem;
		position: absolute;
		right:.384rem;
	}
    .bottom-div{
    	display: flex;
    } 
    .bottom-div .left-logo{
		margin-top: .512rem;
		margin-left: .64rem;
		padding-bottom: .938rem;
		margin-right: .43rem;

	}
	.bottom-div .left-logo img{
		width:2.13rem;
		height:2.13rem;
		border-radius:2.13rem;
		border:2px solid #ffffff;

	}
	.bottom-div .contain-right{
		display: inline-block;
		color:#ffffff;
		font-size: .512rem;
		margin-top: .768rem;
		margin-bottom: .4rem;
	}
	.common-nav-menu{
		width: 100%;
		height: 2.5rem;
		/*line-height: 2.5rem;*/
		background: #f9fdff;
		border-bottom:1px solid #d9e0ec;
		text-align: center;
		display: flex;
		padding:0;
		z-index: 2;
	}
	.common-nav-menu .center-title{
		margin:0;
		padding:0;
		position:relative;
		flex:8;
	}
	.common-nav-menu a{
		line-height: 2.5rem;
		color:#4d4d4d;
		font-size: 18px;
		display: inline-block;
		height:2.5rem;
		width:25%;
		margin:0 1%;
		margin-top: -1px;
		text-align: center;
		margin-top:-1px;
		border-bottom: 2px solid transparent;
	}
	.common-nav-menu .active{
		color:#fe2947;
		border-bottom:2px solid #fe2947;
	}
	.footer{
		position: fixed;
	    left: 0;
	    bottom: 0;
	    width: 100%;
	    height: 50px;
	    background-color: #484d54;
	    color: #fff;
	    z-index: 9000;
	    display: -webkit-box;
	    display: flex;
	}
	.footer .shop{
		position: absolute;
	    top: -8px;
	    left: 6px;
	    width: 50px;
	    height: 50px;
	    border-radius: 50%;
	    background: #3f4349;
	}
	.footer .shop img{
		position: absolute;
		top:11px;
		left:9px;
	}
	.footer .shop .cart-count{
		position: absolute;
	    font-style: normal;
	    width: 20px;
	    height: 20px;
	    top: -5px;
	    right: -5px;
	    background: #fe2947;
	    border-radius: 20px;
	    font-size: 12px;
	    text-align: center;
	    line-height: 20px;
	    z-index: 2;
	}
	.footer .total-money{
		line-height: 50px;
		font-size: 16px;
		margin-left: 73px;

	}
	.footer .choose-ok{
		position: absolute;
		display: block;
	    width: 120px;
	    height: 50px;
	    line-height: 50px;
	    text-align: center;
	    background-color: #fe2947;
	    color: #fff;
	    font-size: 16px;
	    right:0;
	    cursor:pointer;
	}
	.cart-content{
		max-height: 488px;
    	overflow: hidden;
    	position: fixed;
    	bottom:50px;
    	z-index: 8999;
    	width:100%;
    	
	}
	.cart-content ul{
		margin:0;
		padding:0;
        background: #f8f8f8;
		transition-property: transform;
	    transform-origin: 0px 0px 0px;
	    transform: translate(0px, 0px) translateZ(0px);

	}
	.cart-content ul li{
		list-style: none;
		height: 60px;
	    line-height: 60px;
	    border-bottom: 1px solid #e1e3e6;
	    font-size: 14px;
	    margin:0 15px;
	    display: flex;
	}
	.cart-content ul li .cl-r1 {
	    text-overflow: ellipsis;
	    -o-text-overflow: ellipsis;
	    white-space: nowrap;
	    width: 135px;
	    color: #404142;
	    font-size: 14px;
	    height: 50px;
	    overflow: hidden;
	    text-align: left;
	}
	.cart-content ul li .cl-r3{
		width: 60px;
	    color: #fe2947;
	    font-size: 16px;
	    font-weight: 700;
	}
	.cl-r2{
		margin-left: 10px;
	}
	.cl-r2 i{
		display: inline-block;
	    border-radius: 30px;
	    width:8px;
	    border: 1px solid #dadee2;
	    text-align: center;
	    background: #fff;
	    font-size: 15px;
	    font-weight: 700;
	    padding: 6px 10px;
	    margin-bottom: 10px;
	    font-style: normal;
	    line-height: normal;
	    color:red;
	}
	.cart-dark{
		height: 150%;
	    width: 100%;
	    background-color: rgba(0,0,0,.6);
	    position: absolute;
	    z-index: 22;
	    top: 0;
	    left: 0;
	    z-index: 8998;
	}

</style>

