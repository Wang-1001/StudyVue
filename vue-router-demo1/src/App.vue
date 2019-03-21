<template>
  <div id="app" >
		<div class="header">
		
			<router-link to="/" class="nav-itme">
				<img src="./assets/my_class.png" class="logo">
			</router-link>
			
			<router-link to="/task" class="nav-itme" id="nav-itme">任务中心</router-link>
			<router-link to="/taaching" class="nav-itme">教学包</router-link>
			<router-link to="/lib" class="nav-itme">库管理</router-link>
			<router-link to="/questionBank" class="nav-itme">我的题库</router-link>
			<router-link to="/ucenter" class="nav-itme">王德旺</router-link>
		</div>
		<div class="container content"> 
		  <router-view> </router-view>
		</div>
		
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
	
#app {
	background-color: rgb(244,244,244)
} 

.logo{
	width: 125px;
	height: 80%;
}

.header{
		display: flex;
		height: 40px;
		background-color:#fff;
		font-size: 15px;
		padding-left: 200px;
		align-items: center;
}

.nav-itme{
		width: 100px;
		margin-right: 5px;
}
	
#nav-itme{
		margin-left: 30%;
}

.container{
	width: 85%;
	margin: 0 auto;
	height: 1300px;
	
}

a{
	text-decoration: none;
    color: #aaa;
}

a:hover{
	color: rgb(2,165,218);
}

</style>
