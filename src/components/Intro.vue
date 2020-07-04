<template>
	<div id="intro">
		<div class="description">
			<a href="#" class="logo"></a>
			<h1 id="pageTitle"><span>AppStarter.</span> Best landing page for web and mobile apps</h1>
			<div class="btnWrapper">
				<button class="downloadBtn btn">Download Now</button>
				<button class="watchBtn btn">Watch Video</button>
			</div>
		</div>
		<div class="tablet">
			<img src="../img/tablet.png" alt="tablet screenshot">
		</div>
	</div>
</template>

<style scoped lang="scss">
@import '../variables.scss';

#intro {
	@include flex(row, space-between, flex-start);
	padding: 5.2vw 13vw 0 9.375vw;
	
	.description {
		@include flex(column, center, flex-start);
		padding-top: 6.25vw;

		.logo {
			width: 6.25vw;
			height: 6.25vw;
			background: url(../img/logo.svg) no-repeat center;
			background-size: 5.55vw;
			background-color: $light-color;
			box-shadow: 0px 6px 12px rgba(32, 33, 39, 0.08);
			border-radius: 1.3vw;
		}

		#pageTitle {
			width: 38vw;
			margin-top: 2.29vw;
			font-size: 2.43vw;
			font-weight: 300;
			line-height: 3.47vw;
			letter-spacing: 0.07vw;

			span {
				font-weight: 800;
			}
		}

		.btnWrapper {
			@include flex;
			width: 22.98vw;
			padding-top: 2.57vw;

			.btn {
				padding: 0.97vw 1.09vw;
				font-size: 1.18vw;
				letter-spacing: 0.07vw;
				font-weight: 700;
				line-height: 1.598vw;
				border-radius: 0.417vw;
				background: $light-color;

				&:hover {
					cursor: pointer;
					box-shadow: 0.14vw 0.14vw 0.14vw black;
				}

				&:active {
					box-shadow: 0 0 0.44vw black inset;
				}
			}

			.downloadBtn {
				background: linear-gradient(135deg, #ff8e64 0%, #ffe641 100%);
				color: $light-color;
			}
		}
	}

	.tablet {
		padding: 4.35vw 1vw;
		background-color: #fff;
		border-radius: 3.82vw;
		// background-image: linear-gradient(90deg, rgba(255, 255, 255, 0) 0%, rgba(32, 33, 39, 0.03) 100%);
		box-shadow: inset 0 -0.24vw 0.617vw rgba(40, 43, 49, 0.26);

		img {
			height: 40.14vw;
			border: 0.2vw solid #e7e8ea;
			border-radius: 0.42vw;
		}
	}
}

// mobile version
@media (max-width: 700px) {
	#intro {
		@include flex(column);
		padding-top: 0;

		.description {
			align-items: center;

			.logo {
				width: 25vw;
				height: 25vw;
				background-size: 22vw;
				border-radius: 5vw;
			}

			#pageTitle {
				text-align: center;
				width: 80vw;
				font-size: 5vw;
				line-height: 6vw;
				letter-spacing: 0.2vw;
			}

			.btnWrapper {
				width: 66vw;
				padding: 2.57vw 0;

				.btn {
					padding: 3vw 2vw;
					font-size: 4vw;
					letter-spacing: 0.2vw;
					line-height: 5vw;
					border-radius: 2vw;
				}
			}

		}

		.tablet {
			padding: 7.19vw 2.025vw;
			margin-top: 2vw;

			img {
				height: 65vw;
			}
	}
	}
}
</style>