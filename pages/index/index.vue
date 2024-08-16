<template>
    <view class="container">
        <view v-for="(item, index) in list" :key="item.section">
            <uni-section :title="item.section"></uni-section>
            <view v-for="(row, index) in item.rows" :key="row.name">
                <uni-list>
                    <uni-list-item :title="row.name" :clickable="true" :to="row.url"></uni-list-item>
                </uni-list>
            </view>
        </view>
    </view>
</template>

<script lang="ts" setup>
interface ShowItem {
	title: string
	url: string
}

const list = [
	{
		section: "快速开始",
		rows: [
			{
				name: "快速接入",
				url: "/pages/quick/index",
			},
			{
				name: "基础通话",
				url: "/pages/base-call/index",
			},
			{
				name: "自定义通话视图",
				url: "/pages/custom-callview/index",
			},
			{
				name: "自定义挂断弹窗",
				url: "/pages/hangup-comfirm/index",
			},
			{
				name: "自定义下方按钮",
				url: "/pages/custom-bottombar/index",
			},
			{
				name: "视频通话",
				url: "/pages/video-call/index",
			},
			{
				name: "语音通话",
				url: "/pages/voice-call/index",
			},
		],
	},
	{
		section: "调试与配置",
		rows: [
			{
				name: "调试与配置",
				url: "/pages/setting/index",
			},
		],
	},
]

const navigate = (item: ShowItem) => {
	uni.navigateTo({ url: item.url })
}
</script>

<style lang="scss" scoped>
.container {
	padding: 1rem;
	background-color: #F4F4F4;
	.section {
		position: relative;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		margin-top: 10px;
		flex-direction: row;
		align-items: center;
		padding: 0 10px;
		height: 50px;
		background-color: #f8f8f8;
		/* #ifdef APP-NVUE */
		/* #endif */
		font-weight: normal;
	}
}
</style>
