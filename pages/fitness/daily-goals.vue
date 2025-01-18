<template>
	<view class="page">
		<uv-navbar title="Daily Goals" placeholder @leftClick="leftClick"></uv-navbar>
		<lxCalendar />
		<view class="wednesday">
			<view class="">Wednesday</view>
			<view class="">See More</view>
		</view>
		<view class="timeline">
			<view class="timeline-item" v-for="item in 6" :key="item">
				<view class="timeline-item-left">
					<view class="timeline-item-left-time">
						06.00
					</view>
					<view>
						am
					</view>
				</view>
				<view class="timeline-item-right">
					<view class="line"></view>
					<view class="timeline-item-right-card">
						<view class="timeline-item-right-card-icon">

						</view>
						<view class="timeline-item-right-card-center">
							<view>Morning Run</view>
							<view>06.00am - 07.00am</view>
						</view>
						<view class="timeline-item-right-card-right">
							4.50km
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="footer">
			<view class="btn" @click="$refs.popup.open()">
				Add Goals
			</view>
		</view>

		<uv-popup ref="popup" round="24" mode="bottom" @change="change">
			<view class="popup">
				<view class="title">
					Add Goals
				</view>
				<view class="content">
					<view class="formItem">
						<view class="label">
							Goals Title
						</view>
						<view class="formItem-content">
							<input class="input" placeholder="Enter goals name" type="text">
						</view>
					</view>
					<view class="formItem">
						<view class="label">
							Choose Activity
						</view>
						<view class="formItem-content">
							<view class="activityCard">
								<view class="activivtyItem" v-for="item in 8" :key="item"></view>
							</view>
						</view>
					</view>
					<view class="formItem">
						<view class="label">
							Repeat
						</view>
						<view class="formItem-content">
							<view class="selectRepeat">
								<view class="selectRepeat-item" :class="item == form.repeat ?'active' : ''" @click="form.repeat = item" v-for="item in repeatList" :key="item">
									{{ item }}
								</view>
							</view>
						</view>
					</view>
					<view class="formItem">
						<view class="label">
							Select Days
						</view>
						<view class="formItem-content">
							<view class="selectRepeat">
								<view class="selectRepeat-item" :class="item == form.days ?'active' : ''" @click="form.days = item" v-for="item in days" :key="item">
									{{ item }}
								</view>
							</view>
						</view>
					</view>
					<view class="formItem">
						<view class="label">
							Every Days
							<view>
									<uv-switch :model-value="true"></uv-switch>
							</view>
						</view>
					</view>
					<view class="formItem">
						<view class="label">
							Remind me
							<view class="selectTime">
								06.00 am
							</view>
						</view>
					</view>
					
				</view>
				<view class="footer">
					<view class="btn" @click="$refs.popup.open()">
						Add Goals
					</view>
				</view>
			</view>
		</uv-popup>
	</view>
</template>

<script>
	import lxCalendar from '../../components/lx-calendar/lx-calendar.vue'
	export default {
		components: {
			lxCalendar
		},
		data() {
			return {
				form: {
					repeat: 'Daily',
					days: []
				},
				repeatList: ['Daily', 'Weekly', 'Monthly', 'Yearly'],
				days: ['S', 'M', 'T', 'W', 'T', 'F', 'S']
			}
		}
	}
</script>

<style lang="scss" scoped>
	.page {
		padding: 32rpx;
		padding-bottom: 150rpx;
	}

	.popup {
		padding-bottom: 150rpx;
		.btn {
			
		}
		.title {
			padding: 32rpx 0;
			font-size: 32rpx;
			font-weight: bold;
			text-align: center;
		}

		.content {
			padding: 32rpx;

			.formItem {
				margin-bottom: 32rpx;

				.label {
					font-size: 30rpx;
					font-weight: bold;
					display: flex;
					justify-content: space-between;
					align-items: center;
					
					.selectTime {
						padding: 20rpx 32rpx;
						background-color: #f9f9f9;
						border-radius: 100rpx;
						font-weight: normal;
						color: #000;
					}
				}

				.formItem-content {
					margin-top: 32rpx;

					.input {
						padding: 20rpx 32rpx;
						border-radius: 100rpx;
						border: 1px solid #DFE1E7;
					}

					.activityCard {
						padding: 32rpx;
						display: grid;
						grid-template-columns: repeat(4, 1fr);
						background-color: #f9f9f9;
						gap: 20rpx;
						border-radius: 32rpx;
						.activivtyItem {
							width: 140rpx;
							height: 140rpx;
							background: #fff;
							border-radius: 100%;
						}
					}
					
					.selectRepeat {
						display: flex;
						
						.selectRepeat-item {
							flex: 1;
							background-color: #F9F9F9;
							border-radius: 100rpx;
							padding: 20rpx;
							margin-right: 32rpx;
							display: flex;
							justify-content: center;
							align-items: center;
							transition: all;
							color: #818898;
							&.active {
								color: #fff;
								background-color: #0034EE;
							}
						}
					}
				}
			}

		}
	}

	.footer {
		width: 100%;
		height: 150rpx;
		background: #fff;
		padding: 32rpx;
		position: fixed;
		bottom: 0;
		left: 0;

		.btn {
			width: 100%;
			height: 100%;
			background: #0034EE;
			display: flex;
			justify-content: center;
			align-items: center;
			color: #fff;
			border-radius: 100rpx;
		}
	}

	.timeline {
		margin-top: 32rpx;

		&-item {
			display: flex;
			margin-bottom: 32rpx;

			&-left {
				flex-shrink: 0;
				display: flex;
				flex-direction: column;
				align-items: flex-end;

				view:last-child {
					font-size: 26rpx;
					color: #818898;
				}
			}

			&-right {
				flex: 1;
				margin-left: 32rpx;
				padding-top: 18rpx;

				.line {
					width: 100%;
					height: 1px;
					background-color: #ECEFF3;
					margin-bottom: 32rpx;
				}

				&-card {
					background: #F9F9F9;
					padding: 32rpx;
					border-radius: 20rpx;
					display: flex;
					align-items: center;

					&-icon {
						width: 70rpx;
						height: 70rpx;
						background-color: #FFF;
						border-radius: 100%;
						display: flex;
						justify-content: center;
						align-items: center;
						margin-right: 32rpx;
						flex-shrink: 0;
					}


					&-center {
						flex: 1;
						font-size: 30rpx;

						view:first-child {
							font-weight: bold;
							margin-bottom: 5rpx;
						}

						view:last-child {
							font-size: 26rpx;
							color: #818898;
						}
					}

					&-right {
						font-weight: 500;
						font-size: 30rpx;
					}
				}
			}
		}
	}


	.wednesday {
		margin-top: 32rpx;
		display: flex;
		justify-content: space-between;
		align-items: center;

		view:first-child {
			font-size: 38rpx;
			color: #000;
			font-weight: 500;
		}

		view:last-child {
			font-size: 24rpx;
			color: #818898;
		}
	}
</style>