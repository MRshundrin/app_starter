<template>
	<footer id="footerPart">
		<div class="footerTop">
			<a href="#" class="toHome">AppStarter</a>
			<div class="creationWrapper">
				<div>
					<span class="creation">Created with</span>
					<span>by <b>Sergey Azovskiy</b></span>
				</div>     
			</div>
			<div class="socialWrapper">
				<a href="#" class="socialLink twitter"></a>
				<a href="#" class="socialLink facebook"></a>
				<a href="#" class="socialLink instagram"></a>
			</div>
		</div>
		<div class="creationWrapper">© AppStarter, 2017</div>
	</footer>
</template>

<style scoped lang="scss">
@import '../variables.scss';

#footerPart {
	@include flex(column);
	padding: 1.74vw 9.375vw 2.15vw 9.375vw;
	border-top: 0.07vw solid #e7e8ea;

	.footerTop {
		@include flex;
		width: 100%;
	}

	.toHome {
		color: $dark-color;
		font-size: 1.3889vw;
		font-weight: 800;
		line-height: 1.73vw;
	}

	.creationWrapper {
		font-size: 0.764vw;
		color: #999ea8;

		b {
			color: #282b31;
		}

		.creation::after {
			content: ' ';
			display: inline-block;
			vertical-align: sub;
			padding: 0 0.35vw;
			width: 0.98vw;
			height: 0.98vw;
			background: url(../img/like.svg) no-repeat center;
			background-size: 0.98vw;
		}
	}

	.socialWrapper {
		@include flex;
		align-self: flex-end;
		width: 8vw;
		border: 1px solid #e7e8ea;
		border-radius: 0.347vw;

		.twitter {
			background: url(../img/twitter.svg) no-repeat center;
		}
		
		.instagram {
			background: url(../img/insta.svg) no-repeat center;
		}
		.socialLink {
			width: 33.33%;
			height: 2.6vw;
			background-size: 1.5vw 1.3vw;
		}
		.facebook {
			background: url(../img/facebook.svg) no-repeat center;
			background-size: auto 1.12vw;
			border-left: 1px solid #e7e8ea;
			border-right: 1px solid #e7e8ea;
		}
	}
}

// mobile version
@media (max-width: 700px) {
	#footerPart {
		.footerTop {
			@include flex(column, center, center);
		}

		.toHome {
			margin-bottom: 1vw;
			font-size: 3.3889vw;
			font-weight: 800;
			line-height: 3.73vw;
		}

		.creationWrapper {
			font-size: 2.764vw;

			.creation::after {
				width: 2.764vw;
				height: 2.764vw;
				background-size: 2.7vw;
			}
		}

		.socialWrapper {
			margin: 2vw 0;
			align-self: center;
			width: 20.195vw;
			border: 1px solid #e7e8ea;
			border-radius: 1vw;

			.socialLink {
				width: 33.33%;
				height: 6.5vw;
				background-size: 4.11vw 4vw;
			}
		}
	}
}
</style>