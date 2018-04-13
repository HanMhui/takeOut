<template>
	<div class='goods'>
		<div class="left-menu" id='left-menu'>
			<ul v-if='list'>
				<li v-for="(item,index) in list" @click='clickMenu(index)' :class="{'active':index==flg}" :key="index">
					<!-- <a :href="'#menu'+index">{{item.title}}</a> -->
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
		<div class="model-bottom">
		    <div class='multi-content'>
		    	<div class="close"></div>
		    	<div class="multi-title">{{modelData.name}}</div>
		    	<div>
		    		<span>规格:</span>
		    		<div>
		    			<span>8寸</span>
		    			<span>10寸</span>
		    			<span>12寸</span>
		    			<span>14寸</span>
		    			<span>16寸</span>
		    			<span>8寸</span>
		    		</div>
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
			list:[],
			flg:0,
			modelData:{}
		  
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
		},
		scroll(e){
			document.getElementById('menu'+e).scrollIntoView()
		}
	}
}
</script>
<style scoped>
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

		/*margin-top:10px;*/
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
	    z-index: 100001;
	    text-align: center;
	    background-color: #fff;
	    max-height: 100%;
	    overflow: scroll;
	}
	.model-bottom .multi-content{
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
</style>

