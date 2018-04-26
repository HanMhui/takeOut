<template>
	<div>
		<div id='center_content'></div>
		<div class="appraise">
			<div class='appraise-header'>
				<div class="info-num">
					<div class="num">4.8</div>
					<div>整体评价</div>
				</div>
				<div class="info-arrow">
					<div class="info-list">
						<span class="info-list-txt">送餐服务</span>
						<span class="info-list-arrow">
							<span class="arrow-select" style="width:86.4px"></span>
						</span>
						<span class="info-list-num">4.8</span>
					</div>
					<div class="info-list">
						<span class="info-list-txt">菜品质量</span>
						<span class="info-list-arrow">
							<span class="arrow-select" style="width:82.8px"></span>
						</span>
						<span class="info-list-num">4.6</span>
					</div>
				</div>
			</div>
			<div class="comment-title">用户评价</div>
			<div class="shopcomment-list">
				<div class="list-header">
					<div :class='{"active":activName=="全部"}' @click='changeName("全部")'>全部({{appraiseList.total}})</div>
					<div :class='{"active":activName=="有内容"}' @click='changeName("有内容")'>有内容({{appraiseList.content_total}})</div>
				</div>
				<div class='list-content'>
					<ul>
						<li v-for="(item,index) in appraiseList.list" :key='index'>
							<img src="../assets/c1394035.jpeg" class='content-img'>
							<div class="comment-list-title">
								<span class="left">{{item.name}}</span>
								<span class="right f-fr">{{item.date}}</span>
							</div>
							<div class="comment-list-arrow">                
								<span class="info-list-arrow">                    
									<span class="arrow-select" :style="'width:'+70*item.score/5+'px'"></span>                
								</span>                
								<span class="speed">送餐速度：{{item.speed}}</span>            
							</div>
							<div class="comment-container" v-if="item.content">
								{{item.content}}
							</div>
							<div class="comment-zan" v-if="item.zan">                    
								<span></span>                                            
								<span>{{item.zan.join(',')}}</span>                                    
							</div>
						</li>
					</ul>
				</div>
			</div>
		</div>
			
</div>
</template>
<script>
	import axios from 'axios'
	export default{
		data(){
			return{
				activName:"全部",
				appraiseList:{}


			}
		},
		mounted(){
			let m=document.getElementById("head").clientHeight
			let n=document.getElementById("top-div").clientHeight
	        // document.getElementById("left-menu").style.top=m+n+'px'
	        document.getElementById("center_content").style.height=m+n+'px'
	        axios.get('/api/appraise_list').then((res)=>{
		        this.appraiseList=res.data
			})
	        
		},
		methods:{
			changeName(e){
				this.activName=e
				if(e=='有内容'){
					axios.get('/api/appraise_list').then((res)=>{
				        let m=res.data.list
				        let temp=[]
				        for(var i in m){
				        	if(!m[i].content){
				        		temp.push(m[i])
				        	}
				        }
				        this.appraiseList.list=temp
					})
				}else{
					axios.get('/api/appraise_list').then((res)=>{
				        this.appraiseList=res.data
					})
				}

			}

		}
	}
</script>
<style>
	.appraise-header{
		position:relative;
		padding: 15px 15px;

	}
	.info-num {
	    width: 62px;
	    position: absolute;
	    left: 20px;
	    color: #4d4d4d;
	    font-weight: 700;
	    text-align: center;
	    font-size: 15px;
	    margin-top: 5px;
	}
	.info-num .num {
	    font-size: 36px;
	    color: #fe2947;
	    font-weight: 400;
	}
	.info-arrow {
	    margin-left: 93px;
	    color: #333;
	    padding: 0 0 10px 20px;
	    border-left: solid 1px #ccc;
	}
	.info-arrow .info-list {
	    padding-top: 10px;
	}
	.info-arrow .info-list-arrow {
    	display: inline-block;
	    width: 90px;
	    background: url(http://static.waimai.baidu.com/static/mwaimai/images/comment/evaluation_normal@2x_dd1eef2.png) repeat-x;
	    background-size: 18px;
	    height: 18px;
	    position: relative;
	    top: 3px;
	}
	.info-arrow .info-list-arrow .arrow-select {
	    display: inline-block;
	    height: 18px;
	    width: 90px;
	    background: url(http://static.waimai.baidu.com/static/mwaimai/images/comment/evaluation_selected@2x_8c28d85.png) repeat-x;
	    background-size: 18px;
	}
	.comment-title {
	    background: #ecedf1;
	    color: #999;
	    border-top: 1px solid #dbdcde;
	    border-bottom: 1px solid #dbdcde;
	    height: 32px;
	    line-height: 32px;
	    padding: 0 15px;
	}
	.shopcomment-list{
		background: #ffffff;
	}
	.list-header{
		padding:15px;
		overflow: hidden;
	}
	.list-header div{
		float: left;
		width: 48%;
	    height: 100%;
	    border: solid 1px #e0e0e0;
	    color: #656565;
	    height: 35px;
	    text-align: center;
	    line-height: 35px;
	    box-sizing: border-box;
	    border-radius: 3px;
	}
	.list-header .active{
		color:red;
		border:1px solid red;
	}
	.list-header div:first-child{
		margin-right: 2%;
	}
	.list-content ul{
		margin:0;
		padding:0 15px 15px;;
	}
	.list-content li{
		list-style: none;
		position: relative;
	    border-bottom: solid 1px #dbdcde;
	    padding: 15px 0 10px;
	}
	.list-content li:last-child{
		border:0;
	}
	.content-img{
		width: 40px;
	    height: 40px;
	    position: absolute;
	    left: 10px;
	    top: 10px;
	    border-radius: 40px;
	}
	.comment-list-title {
	    color: #333;
	    margin-left: 60px;
    	line-height: 18px;
    	margin-bottom: 10px;
	}
	.comment-list-title .right {
	    float: right;
	    color: #999;
	}
	.comment-list-arrow {
		margin-left: 60px;
    	line-height: 18px;
	    color: #a0a0a0;
	    font-size: 12px;
	}
	.info-list-arrow {
	    display: inline-block;
	    width: 70px;
	    background: url("../assets/evaluation_normal@2x_dd1eef2.png") repeat-x;
	    background-size: 14px;
	    height: 18px;
	    position: relative;
	    top: 6px;
	    margin-bottom: 10px;
	}
	.info-list-arrow .arrow-select {
	    display: inline-block;
	    height: 18px;
	    width: 70px;
	    background: url("../assets/star-red.png") repeat-x;
	    background-size: 14px;
	}
	.comment-container {
	    color: #333;
	    margin-bottom: 10px;
	    margin-left: 60px;
	}
	.comment-zan {
	    color: #999;
	    margin-bottom: 10px;
	    margin-left: 60px;
	}
	.comment-zan span:first-child {
	    background: url("../assets/zan_2655929.png") center center no-repeat;
	    background-size: 10px;
	    display: inline-block;
	    height: 16px;
	    width: 16px;
	    float: left;
	}
	.comment-zan span {
	    margin-right: 5px;
	}



















</style>