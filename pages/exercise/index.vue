<template>
	<view>
		<view class="title" :style="[{'height': customBarH + 'px', 'padding-top': statusBarH + 'px'}]">
			<view class="left">
				<image class="avatar" src="../../static/img/girl-avatar.png"></image>
				<text>莎莎</text>
			</view>
			<view class="right">
				<text class="btn1"></text>
				<text class="btn2"></text>
			</view>
		</view>
		<view class="swipper">
			<bw-swiper :swiperList="swiperList" style="width:100%" swiperType :w_h='swiperW_H' nextMargin='70rpx' previousMargin='70rpx'></bw-swiper>
		</view>
		<view class="content">
			<view class="lesson">
				<view class="lesson-title">陪练课程</view>
				<view class="top">
					<view class="left">
						<view class="time">
							<text class="date">{{lessonDate}}</text>
							<text class="week">{{lessonWeek}}</text>
							<text class="cur-time">{{lessonCurTime}}</text>
						</view>
						<view class="lesson-class">
							<text class="my-lesson">{{myLesson}}</text>
							<text class="lesson-time">{{lessonTime}}</text>
						</view>
					</view>
					<view class="right">
						<view class="avatar" :style="{backgroundImage:`url(${teacherUrl})`}"></view>
						<view class="teacher">{{teacherName}}</view>
					</view>
				</view>
				<view class="bottom">
					<view class="left">
						<text></text>
						评价老师
					</view>
					<view class="right">
						<text></text>
						上传乐谱
					</view> 
				</view>
			</view>
			<view class="know-title">了解大音悦家</view>
			<view class="know-more">
				<view class="container" :style="{width:konwMoreArr.length * 332 + 'rpx'}">
					<view class="more" v-for="(item,index) in konwMoreArr" :key="index">
						<image :src="item.url">
						</image>
						<text class="top">{{item.title}}</text>
						<text class="bottom">{{item.detail}}</text>
					</view>
				</view>

			</view>
		</view>
	</view>

</template>

<script>
	import bwSwiper from '../../wxcomponents/bw-swiper/bw-swiper.vue';
	export default {
		data() {
			return {
				swiperW_H:1.4,
				customBarH: this.customBar,
				statusBarH: this.statusBar,
				teacherUrl:'../../static/img/girl-avatar.png',
				swiperList: [{
					img: 'https://dss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3282090074,2186583189&fm=26&gp=0.jpg',
					text: '加油',
				}, {
					img: 'https://dss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1529929594,4168177509&fm=26&gp=0.jpg',
					text: '加油',
				}, {
					img: 'https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=1907062981,2248939937&fm=26&gp=0.jpg',
					text: '加油',
				}],
				lessonDate: '6月27日',
				lessonWeek: '周六',
				lessonCurTime: '14:00',
				lessonTime: '60分钟',
				myLesson: '钢琴',
				teacherName: '任老师',
				konwMoreArr: [{
						url: '../../static/img/class-guide-bk.png',
						link: '',
						title:'上课指南',
						detail:'陪练流程'
					}, {
						url: '../../static/img/teacher-bk.png',
						link: '',
						title:'师资介绍',
						detail:'顶尖老师在线教学'
					}, {
						url: '../../static/img/know-app-bk.png',
						link: '',
						title:'了解大音悦家',
						detail:'让孩子在家也能上课'
					}

				]

			}
		},
		components: {
			bwSwiper,
		}
	}
</script>

<style lang="less">
	.title {
		width: 750rpx;
		background-color: #fff;
		display: flex;
		justify-content: space-between;
		box-shadow:0px 2px 4px 0px rgba(0,0,0,0.05);
		.left {
			width: 100%;
			height: 100%;
			display: flex;
			align-items: center;
			justify-content: flex-start;

			.avatar {
				display: inline-block;
				width: 70rpx;
				height: 70rpx;
				border-radius: 50%;
				border: 1px solid #ccc;
				margin-left: 40rpx;
				margin-right: 20rpx;
			}
		}

		.right {
			width: 100%;
			height: 100%;
			display: flex;
			align-items: center;
			justify-content: flex-end;

			.btn1,
			.btn2 {
				display: inline-block;
				width: 40rpx;
				height: 40rpx;
				background-size: 100% 100%; 
			}

			.btn1 {
				background-image: url(../../static/img/customer-service.png);
				margin-right:30rpx;
			}

			.btn2 {
				background-image: url(../../static/img/lesson.png);
				margin-right:40rpx;
			}
		}

	}

	.swipper {
		margin-top: 30rpx;
	}

	.content {
		margin-top: 60rpx;
		width: 750rpx;
		box-sizing: border-box;
		padding: 0 40rpx;
		background: #fff;

		.lesson {
			width: 100%;
			box-sizing: border-box;

			.lesson-title {
				background: #fff;
				padding-bottom: 20rpx;
				font-size:17px;
				font-family:PingFang-SC-Bold;
				font-weight:bold;
				color:rgba(51,51,51,1);
			}

			.top { 
				position: relative;
				display: flex;
				justify-content: space-between;
				background:rgba(255,255,255,1);
				box-shadow:0px 0px 8px 0px rgba(0,0,0,0.05);
				border-radius:5px 5px 0px 0px;
				.left {
					padding: 20rpx;
					.time,
					.lesson-class {
						padding: 10rpx 0;
						font-family:PingFang-SC-Medium,PingFang-SC;
						font-weight:500;
						color:rgba(51,51,51,1);
						text {
							margin-right: 20rpx;
						}
					}
					.time{
						font-size: 32rpx;
						.week{
							display: inline-block;
							text-align: center; 
							width:76rpx;
							height:34rpx;
							background:rgba(78,170,237,1);
							border-radius:9px;
							font-size:24rpx; 
							color:#fff;
						}
					}
					.lesson-class{
						font-size: 30rpx;
						.lesson-time{
							font-size: 24rpx;
						}
					}
				}

				.right {
					padding: 20rpx;
					display: flex;
					flex-direction: column;
					justify-content: center;
					align-items: center;
					font-size: 24rpx;
					font-family:PingFang-SC-Medium,PingFang-SC;
					font-weight:500;
					color:rgba(51,51,51,1);;
					.avatar {
						width: 76rpx;
						height: 76rpx;
						border-radius: 50%; 
						background-size: 100% 100%;

					}
				}
			}

			.bottom {
				
				display: flex;
				align-items: center;
				width: 100%;
				height: 104rpx;
				background:rgba(255,255,255,1);
				box-shadow:0px 0px 8px 0px rgba(0,0,0,0.05);
				border-radius:0px 0px 5px 5px;
				.left,
				.right {
					width: 50%;
					height: 100%; 
					display: flex;
					justify-content: center;
					align-items: center;
					box-shadow: 0.5px 0 0 #eee;
					font-size:32rpx;
					font-family:PingFang-SC-Medium;
					font-weight:500;
					color:rgba(16,142,233,1); 
					text {
						display: inline-block;
						width: 92rpx;
						height: 92rpx;
						border-radius: 50%; 
						margin-right: 10rpx;
						background-size: 100% 100%;
					}
				}
				.left text{
					background-image: url(../../static/img/evaluate-teacher.png);
					
				}
				.right text{
					background-image: url(../../static/img/upload-music.png);
				}

				.right {
					box-shadow:none;
				}
			}
		}
		.know-title{
			margin:72rpx 0rpx 10rpx;
			font-size:17px;
			font-family:PingFang-SC-Bold;
			font-weight:bold;
			color:rgba(51,51,51,1);
		}
		.know-more {
			// padding:20rpx;
			width: 100%;
			height: 300rpx;
			overflow: auto; 
			.container {
				height: 100%;
				.more {
					display: inline-block;
					width: 312rpx;
					height: 192rpx;
					margin-right:10rpx;
					position: relative;
					font-family:PingFang-SC-Medium;
					font-weight:500;
					.top{
						position: absolute;
						top:36rpx;
						left:36rpx;
						font-size:32rpx; 
						color:rgba(51,51,51,1);
					}
					.bottom{
						position: absolute;
						top:84rpx;
						left:36rpx;
						font-size: 24rpx; 
						color:rgba(102,102,102,1);
					}
					image {
						width: 100%;
						height: 100%;
					}
				}
			}

		}
	}
</style>
