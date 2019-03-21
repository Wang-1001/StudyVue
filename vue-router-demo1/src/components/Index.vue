<template>
	<!-- 根容器 -->
	<div class="container">
		<div class="button">
			<div>
				<router-link to="/new_course" class="nav-item">
					<button class="btn">新建班课</button>
				</router-link>
			</div>
			<div>
				<router-link to="/new_course" class="nav-item">
					<button class="btn">加入班课</button>
				</router-link>
			</div>
		</div>

		<div class="class">
			<p>进行中的班课</p>
			<p>{{ courses_ing.length }}个进行中的班课</p>
		</div>

		<hr />

		<div class="course-conainer">
			<div class="course" v-for="(courses, index) in courses_ing" :key="index">
				<div class="course-cover">
					<router-link :to="'/course/' + courses.courseId">
						<img :src="courses.cover" />
					</router-link>
				</div>

				<div class="course-class">
					<p>{{ courses.courseClass }}</p>
				</div>

				<div class="course-name">
					<p class="title">{{ courses.courseName }}</p>
				</div>

				
				<div class="teacher">
					<div class="left">
						<div class="avatar"><img :src="courses.avatar" /></div>
						<div class="username">
							<p>{{ courses.username }}</p>
						</div>
					</div>
					<div class="course-code">
						<p  v-if="loginUserId === courses.userId">
							{{ courses.courseCode }}
						</p>
					</div>
					
				</div>
			</div>
		</div>

		<div class="class">
			<p>已结束的班课</p>
			<p>{{ courses_ed.length }}个已结束中的班课</p>
		</div>

		<hr />

		<div class="course-conainer2">
			<div class="course" v-for="(courses, index) in courses_ed" :key="index">
				<div class="course-cover">
					<router-link :to="'/course/' + courses.courseId">
						<img :src="courses.cover" />
					</router-link>
				</div>

				<div class="course-class">
					<p>{{ courses.courseClass }}</p>
				</div>

				<div class="course-name">
					<p class="title">{{ courses.courseName }}</p>
				</div>

				<div class="teacher">
					<div class="left">
						<div class="avatar"><img :src="courses.avatar" /></div>
						<div class="username">
							<p class="code">{{ courses.username }}</p>
						</div>
					</div>
					<div class="course-code">
						<p class="code" v-if="loginUserId === courses.userId">
							{{ courses.courseCode }}
						</p>
					</div>
					
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Index',
	data() {
		return {
			loginUserId: 1,
			/* courses: [] */

			courses_ing: [],
			courses_ed: []
		};
	},

	methods: {
		deleteCourse: function(courseId, index) {
			var _this = this;
			this.$http({
				method: 'delete',
				url: 'http://localhost:8080/api/course/' + courseId
			}).then(function() {
				alert('班课删除成功');
				_this.courses_ing.splice(index, 1);
			});
		}
	},
	created() {
		var _this = this;

		this.$http.get('http://localhost:8080/api/courses').then(function(response) {
			_this.courses_ing = response.data;
		});

		this.$http.get('http://localhost:8080/api/courses1').then(function(response) {
			_this.courses_ed = response.data;
		});

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

.title {
	font-size: 11px;
	color: #333;
	font-weight: 100;
}

.container {
	padding-top: 20px;
}

.course-conainer {
	margin: 0 auto;
	display: flex;
	flex-wrap: wrap;
	padding-top: 10px;
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

.course-class {
	padding-left: 6px;
	margin-top: -10px;
}

.course-name {
	flex: 1 1 20px;
	padding-left: 6px;
	margin-top: -15px;
}

.teacher {
	display: flex;
	justify-content: space-between;
}

.left {
	display: flex;
	padding-left: 5px;
}

.course-code{
	margin-right: 5px;
}

.avatar img {
	width: 30px;
	height: 30px;
	border-radius: 50%;
	margin-right: 5px;
}

.course-code {
	color: rgb(0, 187, 221);
	float: right;
}

.course-code_ringht {
	margin-top: -15px;
	float: right;
}

.btn_delete {
	width: 50px;
	height: 30px;
	border: 1px solid #fff;
	background-color: rgb(0, 187, 221);
	border-radius: 10px;
	outline: none;
	color: #fff;
	font-size: 16px;
	/* float: right; */
	margin-right: 2px;
	margin-bottom: 2px;
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

.class {
	margin: 0 auto;
	display: flex;
	justify-content: space-between;
}

.course-conainer2 {
	margin: 0 auto;
	display: flex;
	flex-wrap: wrap;
	padding-top: 10px;
	-webkit-filter: grayscale(100%);
	-moz-filter: grayscale(100%);
	-ms-filter: grayscale(100%);
	-o-filter: grayscale(100%);
}
</style>
