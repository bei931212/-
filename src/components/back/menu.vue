<template>
	<div class="manager_home">
		<!-- 侧边栏 -->
		<div class="side">
			<el-menu default-active="" router class="el-menu-vertical-demo" theme="dark">
				<template  v-for="(item,index) in arr">
					<el-submenu :index="item.id" v-if="item.child">
						<template slot="title"><i class="el-icon-message"></i>{{item.name}}</template>
						<el-menu-item-group v-for="items in item.child">
							<el-menu-item :index="items.rule">{{items.name}}</el-menu-item>
						</el-menu-item-group>
					</el-submenu>
				</template>	
			</el-menu>
		</div>

		<div class="right_main">
			<!-- 面包屑导航 -->
			<div class="nav">
			
			</div>
			<!-- 主题内容 -->
			<div class="main">
				<router-view></router-view>
			</div>
		</div>
	</div>
</template>
<script>
import {getMenus} from '../../http/api'
export default{
	data(){
		return{
			arr:[]
		}
	},
	created(){
		var _this=this
		console.log(this.arr)
		console.log(this.arr.length)
		 getMenus().then(function(response){
		 	console.log(response)
		 	if(response.data.success){
		 		_this.arr=response.data.data
		 	}else{
				_this.$message.error(response.data.message);
		 	}
		 })
		
	}
}	
</script>
<style>
.manager_home .side{
	width: 200px;
	position: absolute;
	left: 0;
	top: 0;
	bottom: 0;
	background: #324157;
	overflow-y: scroll;
}
.manager_home .nav{
	height: 50px;
	background: #eef1f6;
}
.manager_home .right_main{
	position: absolute;
	left: 200px;
	top: 0;
	bottom: 0;
	right: 0;
	overflow-x: hidden;
	overflow-y: scroll;
}
</style>