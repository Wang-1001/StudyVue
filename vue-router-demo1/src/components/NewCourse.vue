<template>
	<div class="container">
		
		<!-- <input type="text" placeholder="请输入班课名称" v-model="course.courseName" class="input-box"/>
		<input type="text" placeholder="请输入班级" v-model="course.courseClass" class="input-box"/>
		<input type="text" placeholder="请输入图片地址" v-model="course.cover" class="input-box" />
		<button @click="addCourse(course)" class="btn">确定</button> -->
		<div class="f">
			<p>课程</p>
			<input type="text" placeholder="请输入班课名称" v-model="course.courseName" class="input-box"/>
		</div>
		<div class="f">
			<p >班级</p>
			<input type="text" placeholder="请输入班级" v-model="course.courseClass" class="input-box"/>
		</div>
		<div class="f">
			<p>图片</p>
			<input type="text" placeholder="请输入图片地址" v-model="course.cover" class="input-box" />
		</div>
		
		<div class="button">
			<button @click="addCourse(course)" class="btn">确定</button>
		  
		</div>
	</div>
</template>

<script>
export default {
	name: 'NewCourse',
	data() {
		return {
			loginUserId: 1,
			course: {
				courseName: '',
				courseClass: '',
				cover: ''
			}
		};
	},

	methods: {
		addCourse: function(course) {
			var _this = this;
			this.$http({
				method: 'post',
				url: 'http://localhost:8080/api/course',
				data: {
					userId: _this.loginUserId,
					courseName: course.courseName,
					courseClass: course.courseClass,
					cover: course.cover,
					finished: 0
				}
			}).then(function() {
				alert('新增班课成功');
				_this.$router.push('/');
			});
		},
		
		
	}
};
</script>

<style scoped>
/*scoped 只对本页面 */
p {
	font-size: 12px;
	margin-bottom: 5px;
}
.container {
	display: flex;
	flex-direction: column;
	padding-top: 50px;
    align-items: center;
	background: #fff;
	margin-top: 20px;
	/* justify-content:center;
        align-items: center; */
}
.input-box {
	width: 500px;
	height: 40px;
	margin-bottom: 40px;
	font-size: 14px;
}
/* .button{
		display: flex;
	} */
.input-box {
	width: 500px;
	height: 30px;
	margin-bottom: 30px;
	font-size: 14px;
}

.btn {
	width: 120px;
	height: 40px;
	order: 2px solid rgb(0, 187, 221);
	background-color: #fff;
	border-radius: 8px;
	outline: none;
	color: rgb(0, 187, 221);
	font-size: 16px;
	margin-right: 20px;
}
</style>
