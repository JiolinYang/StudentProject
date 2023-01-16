<template>
	<view class="my-contract">
		我的协议
		<my-tabbar :selected="selected"></my-tabbar>
	</view>
</template>

<script>
	import MyTabbar from '@/common/tabbar/my-tabbar.vue'
	export default {
		data() {
			return {
				selected: 3
			}
		},
		components: {
			MyTabbar
		},
	}
</script>

<style scoped>

</style>

