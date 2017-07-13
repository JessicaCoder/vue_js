<!--<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view></router-view>
    <h1>{{title}}</h1>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>-->


<template>
  <div id="app">
  	<hd msg='something interesting'></hd>
    <h1>{{title}}</h1>
    <input type="text" name="" id="" value="" v-model="newItem" @keyup.enter="addNews" />
    <ul>
    	<li v-for="item in items" :class="{finshed:item.isFinshed}" @click="toggleFinsh(item)">{{item.label}}</li>
    </ul>
    <p>child tells me : {{childWords}}</p>
    <!--<component-a msgfromfather="you die!" v-on:child-tell-me-something-emit="listenToMyBoy"></component-a>-->
    <component-a msgfromfather="you dispatch!" v-on:child-tell-me-something="listenToMyBoy"></component-a>
    <ft></ft>
    
  </div>
</template>

<script>
import Store from './store'
import hd from './header'
import ft from './footer'
import ComponentA from './components/componentA'
export default {
  data:function(){
		return {
			title:'this is a todo list2',
			items:Store.fetch(),
			newItem:'',
			childWords:''
		}
	},
	 events:{
	 	'child-tell-me-something':function(msg){
	 		this.childWords=msg;
	 	}
	 },
	methods:{
		"toggleFinsh":function(item){
			item.isFinshed = !item.isFinshed;
		},
		"addNews":function(){
			this.items.push({
				"label":this.newItem,
				"isFinshed":false
			});
			this.newItem='';
			//vue2.0不支持$broadcast
			this.$broadcast('onAddNew',this.items);
		},
		"listenToMyBoy":function(msg){
			this.childWords=msg
		}
	},
	watch:{
		items:{
			handler:function(items){
				Store.save(items)
			},
			deep:false
		}
	},
	components:{ComponentA,hd,ft}
}
</script>

<style>
html {
 height: 100%;
}
.finshed{text-decoration: underline;}
</style>
