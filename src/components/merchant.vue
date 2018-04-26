<template>
	<div class='merchant'>
		<div id='merchant-content'></div>
		<div class='merchant-content'>
			<div class='merchant-row'>
				<div>
					<span>
						<img src="../assets/clock.png">
					</span>
					<p>00:00-23:59</p>
				</div>
				<div>
					<span>
						<img src="../assets/location.png" class='location'>
					</span>
					<p>哈尔滨市道里区安德街34-2号3单元1层7号</p>
				</div>
				<div>
					<span>
						<img src="../assets/phone.png" class='phone'>
					</span>
					<p>18346559651</p>
				</div>
				<div>
					<span>
						<img src="../assets/sound.png" class='sound'>
					</span>
					<p>
						菜品图片仅供参考，请以收到的实物为准，谢谢
					</p>
				</div>
			</div>
		</div>
		<div class="shopdetail">
			<div>
				<img src="../assets/bright_kitchen_b.png">
				<span>堂食实景</span>
			</div>
			<div>
				<img src="../assets/certification_b.png">
				<span>资质证照</span>
			</div>
			<div>
				<img src="../assets/pay_b.png">
				<span>支持在线支付</span>
			</div>	
		</div>
		<div class="shopdetail">
			<div><span>App专享优惠</span>
			</div>
			<div>
				<img src="../assets/jian_b.png">
				<span>满80减43，满100减53，满130减61（在线支付专享）</span>
			</div>
			<div>
				<img src="../assets/xin_b.png">
				<span>(手机app专享)新用户立减9元，钱包新用户随机最高减8元</span>
			</div>	
			<div>
				<img src="../assets/coupon_b.png">
				<span>(手机app专享)支持使用代金券抵付现金</span>
			</div>	
		</div>
		<div class="bottom-text">配送服务由七彩蝶蛋糕店提供</div>
	</div>
</template>
<script>
	export default{
		data(){
			return{

			}
		},
		mounted(){
			let m=document.getElementById("head").clientHeight
			let n=document.getElementById("top-div").clientHeight
	        // document.getElementById("left-menu").style.top=m+n+'px'
	        document.getElementById("merchant-content").style.height=m+n+'px'
	    }

	} 
</script>
<style>
	.merchant{
		background-color: #ecedf1;
	}
    .merchant-content{
    	/*margin-top: 2px;*/
    	font-size: .64rem;
	    color: #4d4d4d;
	    background: #fff;
	    padding: 0rem .5rem;
	    border-top: 1px solid #dbdcde;
	    border-bottom: 1px solid #dbdcde;
    }
	.merchant-row div{
		position: relative;
	    display: -webkit-box;
	    display: flex;
	    border-bottom: 1px solid #eee;
	    padding-bottom: .64rem;
	}
	.merchant-row span{
		width:.81rem;
		height:.81rem;
		padding: .64rem .75rem 0 .14rem;
	}
	.merchant-row img{
		width:.81rem;
		height:.7776rem;
	}
	.merchant-row .location{
		width:.81rem;
		height:.93rem;
	}
	.merchant-row .phone{
		width:.81rem;
		height:.81rem;
	}
	.merchant-row .sound{
		width:1.046rem;
		height:.81rem;
	}
	.merchant-row  p{
		
		margin:0;
		padding:0;
		padding-top: .64rem;
    	max-width: 12.3rem;
	}
	.shopdetail{
		margin-top: 10px;
	    border-top: 1px solid #dbdcde;
    	border-bottom: 1px solid #dbdcde;
    	background: #ffffff;
    	padding: 0 15px;
	    font-size: .64rem;
    	color: #4d4d4d;
	}
	.shopdetail div{
		display: table;
    	width: 100%;
		padding: 8px 0;
    	border-bottom: 1px solid #eee;
	}
	.shopdetail div:last-child{
		border-bottom:0;
	}
	.shopdetail div img{
	    display: table-cell;
	    width: .81rem;
	    height: .81rem;
	    vertical-align: middle;
	    margin-right: .4rem;
	}
    .shopdetail div span{
	    display: table-cell;
	    width: 100%;
	    vertical-align: middle;
	    line-height: .81rem;
    }
    .bottom-text{
    	text-align: center;
    	margin-top: 10px;
    	color: #999;
    	font-size: 14px;
    	padding-bottom: 20px
    }


















</style>