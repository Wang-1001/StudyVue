<template>
	<div class="container">
		<div class="top">
			<p>班课{{ id }}详情页面</p>
		</div>

		<hr />
		
		<div class="main">
			<div class="course">
				<div class="course-cover">
					<img :src="course.cover" />
				</div>
				
				<div class="course-class">
					<p>班级:&nbsp; {{ course.courseClass }}</p>
				</div>
				
				<div class="course-name">
					<p>课程: &nbsp;{{ course.courseName }}</p>
				</div>
				
				<div class="teacher">
					<!-- <div class="left">
						<div class="avatar"><img :src="course.avatar" /></div>
						<div class="username">
							<p class="code">{{course.username }}</p>
						</div>
					</div> -->
					<div class="course-name">
						<p>班课号: &nbsp;{{ course.courseCode }}</p>
					</div>
					
				</div>
				
			</div>
			
			<div class="right_button">
				<div class="end_class" v-if="loginUserId === course.userId">
					<button type="button" @click="addCourse(course)" class="btn">结束班课</button>
				</div> 
				<div class="end_class" v-if="loginUserId === course.userId">
				    <button @click="deleteCourse(course.courseId, index)" class="btn">删除</button>
				</div>
			</div>
			
		</div>


		
	</div>
</template>

<script>
export default {
	name: 'CourseDetail',
	data() {
		return {
			loginUserId: 1,
			id: this.$route.params.id,
			course: {},
			
		};
	},
	methods: {
		addCourse: function(course) {
			var _this = this;
			this.$http({
				method: 'put',
				url: 'http://localhost:8080/api/course',
				data: {
					userId: _this.loginUserId,
					courseName: course.courseName,
					courseClass: course.courseClass,
					courseId: _this.id,
					cover: course.cover,
					finished: 1,
					
				}
			}).then(function() {
				alert('修改成功');
				_this.$router.push('/');
			});
		},
		
		
		deleteCourse: function(courseId, index) {
			var _this = this;
			this.$http({
				method: 'delete',
				url: 'http://localhost:8080/api/course/' + courseId
			}).then(function() {
				alert('班课删除成功');
				_this.$router.push('/');
			});
			
		},
		
	},
	created() {
		var _this = this;
		this.$http.get('http://localhost:8080/api/course/' + this.id).then(function(response) {
			_this.course = response.data;
		});
		
	}
};
</script>
<style scoped>
	
p {
	font-size: 12px;
	margin-bottom: 5px;
}

.container {
	padding-top: 20px;
}

.main{
	display: flex;
}

.course {
	width: 190px;
	display: flex;
	flex-direction: column;
	margin-right: 20px;
	margin-bottom: 30px;
	background-color: #fff;
	justify-content: center;
}

.course-cover img {
	width: 100%;
	height: 100%;
}

.course-cover img {
	width: 100%;
	height: 100%;
}

.course-class {
	padding-left: 6px;
	margin-top: -10px;
}

.course-name {
	flex: 1 1 20px;
	padding-left: 6px;
	margin-top: -15px;
}

	
.btn {
	width: 120px;
	height: 30px;
	border: 1px solid #fff;
	background-color: rgb(0, 187, 221);
	border-radius: 10px;
	outline: none;
	color: #fff;
	font-size: 16px;
}

.end_class{
	margin-top: 50px;
	margin-left: 50px;
}
</style>
