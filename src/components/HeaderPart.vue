<template>
	<header id="headerPart">
		<Navigation/>
		<Intro/>
	</header>
</template>

<script>
import Navigation from './Navigation.vue'
import Intro from './Intro.vue'
export default {
	name: 'header-part',
	components: {
		Navigation,
		Intro
  }
}
</script>

<style scoped lang="scss">
@import '../variables.scss';

#headerPart {
	height: 50vw;
	background: url(../img/headerBackground.png) no-repeat center;
	background-size: cover;
	color: $light-color;
}

@media (max-width: 700px) {
	#headerPart {
		height: 147vw;
	}
}
</style>