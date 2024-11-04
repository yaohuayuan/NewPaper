<template>
	<view class="content">
		<view class="watermark">计工本2201 王立泽</view>
		<uni-list>
			<uni-list-item
				v-for="(item, index) in news"
				:key="item.id"
				:title="item.title"
				:note="item.summary"
				:thumb="item.cover"
				@click="openinfo(item.post_id)"
				link
				class="list-item"
			>
				<template #extra>
					<image :src="item.author_avatar" class="avatar" />
				</template>
			</uni-list-item>
		</uni-list>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				news: []
			}
		},
		onLoad() {
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news',
				method: 'GET',
				data: {},
				success: res => {
					if (res.data && Array.isArray(res.data)) {
						this.news = res.data;
					}
					console.log('请求成功', res.data);
				},
				fail: () => {
					console.error('请求失败');
				}
			});
		},
		methods: {
			openinfo(id) {
				console.log('Clicked item ID:', id);
				uni.navigateTo({
					url: '../info/info/info?id=' + id,
					success: () => {
						console.log('导航成功');
					},
					fail: (res) => {
						console.log('navigate failed', res);
					}
				});
			}
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

	.list-item {
		margin-bottom: 15px;
		border-radius: 8px;
		background-color: #ffffff;
		box-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
		padding: 15px;
		transition: transform 0.2s;
	}

	.list-item:hover {
		transform: translateY(-2px);
	}

	.avatar {
		width: 50rpx;
		height: 50rpx;
		border-radius: 50%;
		border: 2px solid #e0e0e0; /* 头像边框 */
	}
</style>
