<template>
	<div class="pager">
		<div class='head'>
			<div class='center-title'>{{headData.title}}</div>
			<img :src="headData.favorite" class="favorite">
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
					<a>商品</a>
					<a>评价</a>
					<a>商家</a>
				</div>		
			</div>
		
		</div>

	</div>
</template>

<script>
import axios from 'axios'
export default {
	data () {
		return {
		  headData:{}
		}
	},
	mounted(){
	    axios.get('/api/list').then((res)=>{
	        this.headData=res.data
		})
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
		width:70%;
		margin-left: 15%;
	}
	.common-nav-menu a{
		/*line-height: 2.5rem;*/
		color:#4d4d4d;
		font-size: 18px;
		display: inline-block;
		height:2.5rem;
		
		width:25%;
		margin:0 1%;
		text-align: center;
		border-bottom: 2px solid transparent;
	}
</style>

