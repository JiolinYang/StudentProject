<template>
	<view class="my-card">
		我的
		<my-tabbar :selected="selected"></my-tabbar>
	</view>
</template>

<script>
	import MyTabbar from '@/common/tabbar/my-tabbar.vue'
	export default {
		data() {
			return {
				selected: 4
			}
		},
		components: {
			MyTabbar
		},
	}
</script>

<style scoped>

</style>

