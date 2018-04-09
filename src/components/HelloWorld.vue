<template>
  <div class="hello">
    500
  </div>
</template>

<script>
import axios from 'axios'
export default {
	data () {
		return {
		  
		}
	},
	mounted(){
	    axios.get('/api/list').then((res)=>{
	        // this.cmt = res.data.data;
	        // this.list = res.data.data.list;
	        	console.log(res)
		})
	}
}
</script>

