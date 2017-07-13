<template>
	<div class="head" @click="doThis">
		头部{{username}}
	</div>
</template>

<script>
	export default {
		data:function(){
			return {
				username: 'jsr'
			}
		},
		props: ['msg'],
		methods: {
			"doThis": function() {
				console.log(this.msg);
			}
		}
	}
</script>