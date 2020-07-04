<template>
	<main id="mainPart">
		<h2 class="secondaryTitle"><span>Why</span> do we use it?</h2>
		<p class="secondaryDescription">This sounded nonsense to Alice, so she said nothing, but set off at once toward the Red Queen. To her surprise, she lost sight of her in a moment.</p>
		<Timers/>
	</main>
</template>

<script>
import Timers from './Timers.vue'

export default {
	name: 'main-part',
	components: {
		Timers
	}
}
</script>

<style scoped lang="scss">
@import '../variables.scss';

#mainPart {
	@include flex(column);
	background: #f8f9fa;
	padding: 17.32vw 0 6.4vw;
	
	.secondaryTitle {
		margin-bottom: 1.2vw;
		font-size: 2.43vw;
		font-weight: 300;
		color: $dark-color;
		letter-spacing: 0.07vw;
		line-height: 3.47vw;

		span {
			font-weight: 800;
		}
	}

	.secondaryDescription {
		width: 39.583vw;    
		color: #676c75;
		font-size: 1.111vw;
		line-height: 2.08vw;
		text-align: center;
	}
}

// mobile version
@media (max-width: 700px) {
	#mainPart {
		padding-top: 26vw;
		
		.secondaryTitle {
			font-size: 6.43vw;
			line-height: 8vw;
		}

		.secondaryDescription {
			width: 75.583vw;    
			font-size: 3.111vw;
			line-height: 4.08vw;
		}
	}
}
</style>
