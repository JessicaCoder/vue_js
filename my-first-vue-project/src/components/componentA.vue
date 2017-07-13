<template>
	<div class="hello">
		<h1>{{msg}}</h1>
		<h1>{{msgfromfather}}</h1>
		<button v-on:click="onClickMe">open mouse</button>
	</div>
</template>

<script>
	export default{
		data:function(){
			return {
				msg:'hello from component a !'
			}
		},
		events:{
	 	'onAddNew':function(msg){
	 		console.log(msg);
	 	}
	 },
		props:['msgfromfather'],
		methods:{
			"onClickMe":function(){
				this.$emit("child-tell-me-something",this.msg);
//				vue2.0不支持$dispatch
//				this.$dispatch('child-tell-me-something', this.msg);
			}
		}
	}
</script>

<style scoped>
	h1{color: #42B983;}
</style>