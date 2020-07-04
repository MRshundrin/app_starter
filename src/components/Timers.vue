<template>
	<div id="timersWrapper">
		<form action="submit" id="timerForm" @submit.prevent="submitTimer()">
			<input type="text" id="timerInput" placeholder="Timer Name" v-model="name">
			<button type="submit" class="createBtn btn">Create Timer</button>
		</form>
		<hr noshade>
		<ul id="task-wrapper">
			<li class="timer" v-for="timer in timers" :key="timer.id">
				<span class="timerName">{{ timer.name }}</span>
				<div class="time" :class="{ activeTimer: timer.play }">{{ timer.time }}</div>
				<div class="btnWrapper">
					<button class="pausePlayBtn timerBtn" :class="{ pauseBtn: timer.play }" @click="pausePlayTimer(timer)">
						<img src="../img/pause.svg" alt="pause image" v-if="timer.play">
						<img src="../img/play.svg" alt="play image" v-else>
					</button>
					<button class="deleteBtn timerBtn" @click="deleteTimer(timer)"><img src="../img/delete.svg" alt="pause image"></button>
				</div>
			</li>
		</ul>
	</div>
</template>

<script>
export default {
	name: 'timers',
	data() {
		return {
			timers: [],
			name: null
		}
	},
	mounted() {
		if (localStorage.getItem('timers')) {
			try {
				this.timers = JSON.parse(localStorage.getItem('timers'))
				this.timers.forEach(timer => {
					if (timer.play) {
						this.createNewTime(timer)
						this.timeRunning(timer)
					}
				})
			} catch(e) {
				localStorage.removeItem('timers')
			}
		}
	},
	methods: {
		submitTimer() {
			if (this.name == null) {
				this.name = Date()
			}
			this.timers.unshift({id: Date.now(), lastDate: Date.now(), name: this.name, millisec: 0, sec: 0, min: 0, hour: 0, time: `00:00:00`, play: true, started: '' })
			this.timeRunning(this.timers[0])
			this.name = null
			this.saveTimers()
		},

		saveTimers() {
			const parsed = JSON.stringify(this.timers)
			localStorage.setItem('timers', parsed)
		},

		deleteTimer(timer) {
			const index = this.timers.findIndex(n => n.id === timer.id)
			if (index !== -1) {
				this.timers.splice(index, 1)
			}
		},

		pausePlayTimer(timer) {
			timer.play = !timer.play
			this.timeRunning(timer)
		},

		timeRunning(timer) {
			if (timer.play) {
				timer.started = setInterval(() => {
					timer.sec++
					timer.millisec += 1000
					timer.lastDate = Date.now()
					
					if (timer.sec > 59) {
						timer.sec = 0
						timer.min++
					}

					if (timer.min > 59) {
						timer.min = 0
						timer.hour++
					}
					
					let zero = (num) => {
						if (num < 10) {
							return '0' + String(num)
						} else {
							return num
						}
					}
					
					timer.time = `${zero(timer.hour)}:${zero(timer.min)}:${zero(timer.sec)}`
					
				}, 1000)
			} else {
				clearInterval(timer.started)
			}
		},

		createNewTime(timer) {
			let timeDifference = Date.now() - timer.lastDate + timer.millisec
			timer.sec = parseInt((timeDifference / 1000) % 60)
			timer.min = parseInt((timeDifference / (1000 * 60)) % 60)
			timer.hour = parseInt((timeDifference / (1000 * 60 * 60)) % 24)			
		}
	},
	
	watch: {
		timers: {
			handler: function () {
				this.saveTimers()
			},
			deep: true
		}
	}
}
</script>

<style scoped lang="scss">
@import '../variables.scss';

#timersWrapper {
	@include flex(column);
	width: 53.472vw;
	padding: 2.778vw 0;
	margin-top: 4.167vw;
	background: $light-color;
	border-radius: 0.833vw;

	hr {
		background-color: #e7e8ea;
		height: 1px;
		margin: 0;
		width: 100%;
		border: none;
		margin-bottom: 0.694vw;
	}

	#timerForm {
		@include flex;
		width: 34.02vw;
		padding-bottom: 2.083vw;

		#timerInput {
			width: 19.583vw;
			height: 3.472vw;
			padding: 0 0 0 1.389vw;
			border: none;
			border: 1px solid #e7e8ea;
			border-radius: 0.417vw;
			background-color: #f8f9fa;
			font-family: "Nunito Sans";
			font-size: 1.18vw;
			color: rgba(103, 108, 117, 0.9);

			&::placeholder {
				color: rgba(103, 108, 117, 0.7);;
			}

			&:focus {
				outline: none;
			}
		}

		.createBtn {
			padding: 0.9vw 1.8053vw;
			font-size: 1.18vw;
			letter-spacing: 0.07vw;
			font-weight: 700;
			line-height: 1.6667vw;
			border-radius: 0.417vw;
			background: linear-gradient(135deg, #ff8e64 0%, #ffe641 100%);
			color: $light-color;

			&:hover {
				cursor: pointer;
				box-shadow: 0.14vw 0.14vw 0.14vw black;
			}

			&:active {
				box-shadow: 0 0 0.44vw black inset;
			}
		}
	}

	.timer {
		@include flex(row, flex-start);
		width: 34vw;
		padding: 1.3889vw 0;

		.timerName {
			width: 10vw;
			padding-right: 3vw;
			white-space: nowrap;
			color: #5586f2;
			font-size: 1.389vw;
			font-weight: 800;
			line-height: 2vw;
			overflow: hidden;
			text-overflow: ellipsis;
		}

		.time {
			width: 8.125vw;
			height: 3.472vw;
			padding: 0.972vw 1.667vw;
			margin-right: 3vw;
			box-sizing: border-box;
			background-color: #ffe4eb;
			border-radius: 0.42vw;
			color: #676c75;
			font-size: 1.18vw;
			text-align: center;
		}

		.activeTimer {
			background-color: #e7e8ea;
		}

		.btnWrapper {
			@include flex;
			width: 8.333vw;

			img {
				height: 2vw;
			}

			.timerBtn {
				width: 3.472vw;
				height: 3.472vw;
				box-sizing: border-box;
				padding: 0.736vw;
				line-height: 2vw;
			}

			.pausePlayBtn {
				border-radius: 50%;
				line-height: 2vw;
				background: linear-gradient(135deg, #009fc5 0%, #3cecb0 100%);
			}

			.pauseBtn {
				background: linear-gradient(135deg, #7956ec 0%, #2fb9f8 100%);
			}

			.deleteBtn {
				border-radius: 0.416vw;
				background: linear-gradient(135deg, #f23673 0%, #fca069 100%);
			}
		}
	}
}

// mobile version
@media (max-width: 700px) {
	#timersWrapper {
		width: 90vw;
		border-radius: 3.833vw;

		#timerForm {
			width: 75vw;
			
			#timerInput {
				width: 45vw;
				height: 8.472vw;
				border-radius: 1.417vw;
				font-size: 3.18vw;
			}

			.createBtn {
				padding: 2.646vw 1.8053vw;
				font-size: 3.18vw;
				letter-spacing: 0.14vw;
				line-height: 3.18vw;
				border-radius: 1.417vw;
			}
		}

		.timer {
			width: 75vw;

			.timerName {
				width: 19.7vw;
				font-size: 3vw;
				line-height: 4.9vw;
			}

			.time {
				width: 22.875vw;
				height: 6.62vw;
				padding: 1.69vw 1.667vw;
				font-size: 3.242vw;
				line-height: 3.242vw;
			}

			.btnWrapper {
				width: 15.333vw;

				img {
					height: 3.8vw;
				}

				.timerBtn {
					width: 6.62vw;
					height: 6.62vw;
					line-height: 3.8vw;
				}

				.deleteBtn {
					border-radius: 1vw;
				}
			}
		}
	}
}
</style>