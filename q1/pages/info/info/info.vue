<template>
	<view class="content">
		<view class="watermark">计工本2201 徐昌盛</view>
		<view class="title">
			{{title}}
		</view>
		<view class="art_conten">
			<rich-text :nodes="strings"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '',
				strings: ''
			}
		},
		onLoad(options) {
			this.id = options.id; // 获取传递的 ID
			console.log('Received ID:', this.id);
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news/36kr/'+this.id,
				method: 'GET',
				data: {},
				success: res => {
					console.log(res)
					this.title = res.data.title;
					this.strings = res.data.content;
				},
				fail: () => {
					console.error('请求失败');
				}
			});
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 20px;
		background-color: #f9f9f9;
		border-radius: 10px;
		box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
	}

	.watermark {
		position: absolute;
		bottom: 10px;
		right: 10px;
		color: rgba(0, 0, 0, 0.1);
		font-size: 18px;
		animation: float 5s linear infinite;
	}

	@keyframes float {
		0% { transform: translateY(0); }
		50% { transform: translateY(-5px); }
		100% { transform: translateY(0); }
	}

	.title {
		font-size: 24px;
		font-weight: bold;
		margin-bottom: 20px;
		color: #333;
		text-align: center;
	}

	.art_conten {
		width: 100%;
		max-width: 600px; /* 限制内容最大宽度 */
		line-height: 1.6; /* 增加行间距 */
		color: #555;
		background-color: #fff; /* 背景颜色 */
		padding: 15px;
		border-radius: 5px; /* 圆角 */
		box-shadow: 0 1px 5px rgba(0, 0, 0, 0.1); /* 阴影效果 */
	}
</style>
