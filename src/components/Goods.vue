<template>
	<div class='goods'>
		<div class="left-menu" id='left-menu'>
			<ul v-if='list'>
				<li v-for="(item,index) in list" @click='clickMenu(index)' :class="{'active':index==flg}" :key="index">
					<a @click='scroll(index)'>{{item.title}}</a>
				</li>
			</ul>
		</div>
		<div class="list" id='list'>
			<ul v-for="(items,index) in list" :id="'menu'+index" :name="'menu'+index">
				<li v-for='item in items.children'>
					<div class='warp'>
					    <div class='img'><img :src='item.img'></div>
						<div class='list-content'>
							<h4 class='title'>{{item.name}}</h4>
							<div class="description">已售出{{item.sold}}份</div>
							<div class="price">￥{{item.price}}</div>
						</div>
						<div class="item-muli" @click='showModel(item)'>可选规格</div>
					</div>
				</li>
			</ul>
		</div>
		<div class="model-bottom" v-show='bottomShow'>
		    <div class='multi-content'>
		    	<div class="close"></div>
		    	<div class="multi-title">{{modelData.name}}</div>
		    	<div>
		    		<span style="float:left;padding-top:5px">规格:</span>
		    		<div class="size">
		    			<span v-for='(item,index) in modelData.size' :class='{"colorRed":index==sizeIndex}' @click='changeSize(index)'>{{item}}</span>
		    		</div>
		    	</div>
		    	<div class="multi-name">
		    		<span>价格:</span>
		    		<span style="color:red;">￥{{modelData.price}}</span>
		    	</div>
		    	<div class="multi-name">
		    		<span>数量:</span>
		    		<span>
			    		<i :class='{"colorRed":num>1}' @click='plusNum'>-</i>
			    		<span style="padding:0 10px;">{{num}}</span>
			    		<i class='colorRed' @click='addNum'>+</i>
		    		</span>
		    	</div>
		    	<div class="multi-btn" @click='addCart'>加入购物车</div>
		    </div>
		</div>
	    <div class='mul-mark' v-show='bottomShow' @click='bottomShow=false'></div>
	</div>
</template>

<script>
import axios from 'axios'
export default {
	data () {
		return {
			list:[],
			flg:0,
			modelData:{},
			bottomShow:false,
			num:1,
			cartData:[],
			sizeIndex:0,
			size:"",
			numtotal:0,
		}
	},
	mounted(){
		let m=document.getElementById("head").clientHeight
		let n=document.getElementById("top-div").clientHeight
        document.getElementById("left-menu").style.top=m+n+'px'
        document.getElementById("list").style.marginTop=m+n+'px'
        axios.get('/api/list').then((res)=>{
	        this.list=res.data
		})
	},
	methods:{
		clickMenu(index){
			this.flg=index;
		},
		showModel(e){
           this.modelData=e
           this.num=1
           this.sizeIndex=0
           this.bottomShow=true;
		},
		scroll(e){
			document.getElementById('menu'+e).scrollIntoView()
		},
		addNum(){
			this.num=this.num+1
		},
		plusNum(){
			this.num>1 ? this.num=this.num-1:this.num
		},
		addCart(){
			let temp={
				"name":this.modelData.name,
				"price":this.modelData.price,
				"num":this.num,
				"size":this.size?this.size:this.modelData.size[0]
			}
			this.numtotal=this.numtotal+this.num
			let flg=0
			for (var i=0;i<this.cartData.length;i++){
				if(this.cartData[i].name==temp.name){
					flg=1
					this.cartData[i].num=this.cartData[i].num+temp.num
				}
			}
			if (flg==0)
				this.cartData.push(temp)
			let temp1={
				'numtotal':this.numtotal,
				'cartData':this.cartData
			}
			this.$emit('changenums',temp1);
			this.bottomShow=false;
		},
		changeSize(index){
			this.sizeIndex=index;
			this.size=this.modelData.size[index]
		}
	}
}
</script>
<style>
	.goods ul{
		margin:0;
		padding:0;
	}
	.goods li{
		list-style: none;
	}
	.goods .left-menu{
		position: fixed;
		z-index: -1;
	    left: 0;
	    width: 25%;
	    bottom: 0;
	    padding-bottom: 70px;
	    background: #ebedf0;
	    overflow-y: auto;
	}
	.goods .left-menu li a{
		display: inline-block;
		width:100%;
		text-align: center;
		height:45px;
		line-height: 46px;
		color:#4d4d4d;
		border-bottom: 1px solid #eee;
		text-decoration: none;
	}
     .goods .left-menu{
     	z-index: 2;
     }
	.goods .list{
		margin-left: 25%;
	}
	.goods .list ul{
		margin-left:10px;
	}
	.goods .left-menu .active a{
        color:#ff2e4b;
        border-left: 3px solid #fd687d;
    	background-color: #fff;
	}
	.goods .list .warp{
		border-bottom: 1px solid #eee;
	    padding: 10px 0;
	    position: relative;
	    display: flex;
	}
	.goods .list .warp .img{
		
	    margin-left: 10px;
	    margin-top: 10px;
	}
	.goods .list .warp img{
		width:50px;
		height:50px;
	}
	.goods .list-content{
		flex:1;
		margin-left: 10px;
	}
	.goods .list-content .title{
		margin:0;
		margin-top:5px;
		padding:0;
		color: #4d4d4d;
	    font-size: .7rem;
	    font-weight: 400;
	    width: 8rem;
	    overflow: hidden;
	    text-overflow: ellipsis;
	    -o-text-overflow: ellipsis;
	    white-space: nowrap;
	}
	.goods .list-content .description{
		color: #999;
    	font-size: 12px;
	}
	.goods .list-content .price{
		color: #ff2e4b;
    	font-size: 15px;
    	font-weight: 700;
	}
	.goods .item-muli{
		position: absolute;
	    right: 0;
	    bottom: 5px;
	    overflow: hidden;
	    border: 1px solid #dadee2;
	    border-radius: 20px;
	    color: red;
	    font-size: 12px;
	    padding: 1px 4px;
	}
	.model-bottom{
		width: 100%;
	    position: fixed;
	    left: 0;
	    bottom: 0;
	    text-align: center;
	    background-color: #fff;
	    max-height: 100%;
	    overflow: scroll;
	    z-index: 10000;
	}
	.multi-content{
		font-size: 16px;
	    text-align: left;
	    width: 90%;
	    margin-left: 5%;
	    padding-top: 20px;
	    font-weight: 100;
	    color: #333;
	    padding-bottom: 40px;

	}
	.model-bottom .close{
		cursor: pointer;
	    background: url(http://static.waimai.baidu.com/static/mwaimai/images/search_close_icon_c5f968d.png) no-repeat;
	    width: 18px;
	    height: 18px;
	    position: absolute;
	    top: 10px;
	    padding: 20px 20px 20px 0;
	    right: 0;
	}
	.model-bottom .multi-title{
		font-size: 18px;
	}
	.mul-mark{
		width: 100%;
    	height: 100%;
	    position: fixed;
	    top: 0;
	    left: 0;
	    text-align: center;
	    background-color: rgba(125,126,127,.5);
	    z-index: 9999;
	}
	.size{
		margin:30px 0;
		margin-left: 50px;
	}
	.size span{
		display: inline-block;
	    border-radius: 10px;
	    border: 1px solid #dadee2;
	    text-align: center;
	    background: #fff;
	    font-size: 15px;
	    font-weight: 700;
	    padding: 4px 6px;
	    margin-left: 6px;
	    margin-bottom: 10px;
	    font-style: normal;
	}
	.multi-name{
		margin: 30px 0;
	}
	.multi-name i{
		display: inline-block;
	    border-radius: 30px;
	    width:8px;
	    border: 1px solid #dadee2;
	    text-align: center;
	    background: #fff;
	    font-size: 15px;
	    font-weight: 700;
	    padding: 6px 10px;
	    margin-left: 6px;
	    margin-bottom: 10px;
	    font-style: normal;
	}
	.colorRed{
		color:red!important;
		border:1px solid red!important;
	}
	.multi-btn{
		height: 30px;
	    width: 98%;
	    margin-left: 1%;
	    font-size: 20px;
	    background-color: red;
	    padding: 5px 0;
	    border-radius: 4px;
	    color: #fff;
	    bottom: 15px;
	    text-align: center;
	    cursor:pointer;
	}
</style>

