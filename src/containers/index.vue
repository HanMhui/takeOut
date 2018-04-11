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
					<a :class="{ active: isActive }">商品</a>
					<a>评价</a>
					<a>商家</a>
				</div>		
			</div>
		</div>
	    <component :is='component' id='content-component'></component>



		<div class='footer'>
		   	<div class='shop'>
		   		<div class='cart-count'>1</div>
		   		<img src='../assets/shop.png'>
		   	</div>
		   	<span class='total-money'>共￥100元</span>
		   	<span class='choose-ok' >选好了</span>

		</div>

	</div>
</template>

<script>
import Goods from '../components/Goods'
import axios from 'axios'
export default {
	data () {
		return {
			headData:{},
			isActive:true,
			component:"Goods"

		}
	},
	components:{
		"Goods":Goods
    },
	mounted(){
	    axios.get('/api/head').then((res)=>{
	        this.headData=res.data
		})
		// let m=document.getElementById("head").clientHeight
		// console.log(m)
		// let n=document.getElementById("top-div").clientHeight
		// console.log(n)
		// document.getElementById('content-component').style.marginTop=m+n+'px'
	},
	methods:{
		// aa(){
		// 	let m=document.getElementById("head").offsetHeight
		// 	console.log(m)
		// }
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
</style>

