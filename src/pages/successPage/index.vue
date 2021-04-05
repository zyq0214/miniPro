<template>
  <view class="page" >
	<view class="weui-msg">
		<view class="weui-msg__icon-area"><i class="weui-icon-success weui-icon_msg"></i></view>
		<view class="weui-msg__text-area">
			<h2 class="weui-msg__title">操作成功</h2>
			<view class="weui-msg__desc">您的信息已登记成功，可点击下方的按钮继续进行发布操作</view>
		</view>
		<view class="weui-msg__opr-area">
			<view class="weui-btn-area">
				<a href="javascript:history.back();" class="weui-btn weui-btn_primary" @click="handleClick()">前往发布</a>
			</view>
		</view>
		<view class="weui-msg__tips-area">
			<view class="weui-msg__tips">可以在user->我的仓库/货车/货物界面查看已登记的信息并进行删除/修改/发布等操作</view>
		</view>
		<view class="weui-msg__extra-area">
			<view class="weui-footer">
				<view class="weui-footer__links">
					<a class="weui-footer__link">底部链接文本</a>
				</view>
				<view class="weui-footer__text">Copyright &copy; 2008-2016 weui.io</view>
			</view>
		</view>
	</view>
</view>

</template>

<script>
export default {
    methods: {
		handleClick() {
			mpvue.navigateTo({url: '/pages/searchResult/main'})
		}
	}
}
</script>

<style scoped>

</style>