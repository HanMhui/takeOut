<template>
	<div>
		<div id='merchant-content'></div>
		hgggjhgjhg
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