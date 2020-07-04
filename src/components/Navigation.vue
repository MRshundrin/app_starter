<template>
  <div id="navbar">
		<a href="#" class="toHome">AppStarter</a>
		<transition name="slide">
			<nav id="navigation" v-if="mobileMenu || !mobile">
				<button id="close-menu-btn" @click="menu" v-if="mobile && mobileMenu"><img src="../img/close.svg" alt="menu"></button>
				<a href="#">Features</a>
				<a href="#">Video Tour</a>
				<a href="#">Reviews</a>
				<a href="#">Pricing</a>
				<a href="#" class="getFree">get it free</a>
			</nav>
		</transition>
		<button id="mobile-btn-menu" @click="menu" v-if="mobile"><img src="../img/menu.svg" alt="menu"></button>
  </div>
</template>

<script>
export default {
	name: 'navigation',
	data() {
		return {
			mobile: false,
			mobileMenu: false,
			windowWidth: window.innerWidth
		}
	},
  
  methods: {
    menu () {
      if (this.mobile) {
        this.mobileMenu = !this.mobileMenu
      }
    }
  },
  mounted () {
    window.onresize = () => {
      this.windowWidth = window.innerWidth;
      if (this.windowWidth > 700) {
        this.mobile = false;
      } else {
        this.mobile = true;
      }
    };
  },
}
</script>

<style scoped lang="scss">
@import '../variables.scss';

#navbar {
	@include flex;
	padding: 1.74vw 9.375vw 0 9.375vw;

	.toHome {
		font-size: 1.3889vw;
		font-weight: 800;
	}

	#navigation {
		@include flex;
		width: 34vw;
	}

	.getFree {
		background-color: $light-color;
		color: $dark-color;
		font-weight: 700;
		text-transform: uppercase;
		border-radius: 0.42vw;
		padding: 0.7vw 1.49vw;

		&:hover {
			text-shadow: none;
			background: linear-gradient(135deg, #ff8e64 0%, #ffe641 100%);
		}

		&:active {
			box-shadow: 0 0  0.42vw $light-color inset;
		}
	}
	
	a {
		font-size: 1.04vw;

		&:hover {
			text-shadow: 1px 1px 1px black;
		}
	}
}

// mobile version
@media (max-width: 700px) {
	.slide-enter-active,
	.slide-leave-active
	{
		transition: transform 0.3s ease;
	}

	.slide-enter,
	.slide-leave-to {
		transform: translateX(200%);
		transition: all 200ms ease-in 0s
	}

	#close-menu-btn, #mobile-btn-menu {
		width: 10vw;
		height: 10vw;
		margin: 5vw;
		align-self: flex-end;

		img {
			width: 100%;
		}
	}
	
	#navbar {
		.toHome {
			font-size: 5vw;
		}

		#navigation {
			@include flex(column, flex-start);
			width: 100%;
			height: 100vh;
			background: #6079f1;
			position: absolute;
			right: 0;
			top: 0;

			a {
				text-align: center;
				width: 100%;
				font-size: 12vw;
				box-sizing: border-box;
				padding: 2vw 5vw;
			}
		}
	}
}
</style>
