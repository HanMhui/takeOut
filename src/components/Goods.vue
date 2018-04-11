<template>
	<div class='goods'>
		<div class="left-menu" id='left-menu'>
			<ul v-if='list'>
				<li v-for="(item,index) in list" @click='clickMenu(index)' :class="{'active':index==flg}" :key="index">
					<a :href="'#menu'+index">{{item.title}}</a>
				</li>
			</ul>
		</div>
		<div class="list" id='list'>
			<ul v-for="(items,index) in list" :id="'menu'+index">
				<li v-for='item in items.children'>
				<!-- {{item.price}} -->
				<div class='warp'>
					<img :src='item.img'>
					<div class='list-content'>
						<h4 class='title'>{{item.name}}</h4>
					</div>
				</div>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
import axios from 'axios'
export default {
	data () {
		return {
			list:[],
			flg:0
		  
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

	 //    axios.get('/api/list').then((res)=>{
	 //        // this.cmt = res.data.data;
	 //        // this.list = res.data.data.list;
	 //        	console.log(res)
		// })
	},
	methods:{
		clickMenu(index){
			this.flg=index;
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
	}
	.goods .list .warp img{
		width:50px;
		height:50px;
	    margin-left: 10px;
	    margin-top: 10px;
	}
</style>

