<template>
	<div>
		123
		{{ this.$store.state.lists }}
	</div>
</template>
<script>
	import axios from 'axios'
	export default {
		/**
		 * [SSR获取所有组件的asyncData并执行获得初始数据]
		 * @param  {[Object]} store [Vuex Store]
		 * 此函数会在组件实例化之前调用，所以它无法访问 this。需要将 store 和路由信息作为参数传递进去：
		 */
		asyncData (store, route) {
			// console.log(store)
			// return Promise.all([
				return store.dispatch('fetchLists');
			// ]);
		},
		name: "home",
		// 数据
		data() {
			return {
				page: 1, // 页码
				test: []
			}
		},
		// 计算属性
		computed: {
	      lists () {
	        return this.$store.getters.getLists // 文章列表
	      },
		},
		// beforeMount () {
		// 	if (this.$root._isMounted) {
		// 		console.warn(this.$root)
		// 		this.fetchLists()
		// 	}
		// },
		mounted() {
			// 不需要SSR的数据在这里请求
			// axios.get('https://cnodejs.org/api/v1/topics?tab=ask')
			// .then((res) => {
			// 	console.warn('mounted', res.data)
			// 	this.test = res.data.data
			// })
		},
		// 方法
		methods: {
			// fetchLists () {
			// 	this.$store.dispatch('fetchLists', { page: 1 }) // 服务端渲染触发
			// },
			pageChange (type) {
			
			},
			goArticle (articleId) {
				this.$router.push({path: '/detail', query: {id: articleId}});
			}
		},
		// 子组件
		components: {
		}
	}
</script>
<!--当前组件的样式 -->
<style scoped>
.ul_box{
	margin-top: 25px;
}
.one_article{
	height: 50px;
	line-height: 50px;
	padding: 0 20px 0 80px;
	border-bottom: 1px solid #ccc;
	list-style: none;
	background: #fff;
	font-size: 14px;
	position: relative;
}
.one_article p{
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
}
.one_article .count{
	font-size: 12px;
	display: inline-block;
	width: 120px;
}
.user_img{
	width: 40px;
	height: 40px;
	position: absolute;
	top: 50%;
	left: 20px;
	transform: translateY(-50%);
}
.btn_box{
	width: 240px;
	margin: 20px auto;
}
.btn_box:after{
	content: '';
	display: block;
	clear: both;
}
.page_btn{
	width: 100px;
	height: 40px;
	margin: 0 10px;
	line-height: 40px;
	font-size: 14px;
	text-align: center;
	color: #80bd01;
	background: #fff;
	float: left;
	cursor: pointer;
}
</style>