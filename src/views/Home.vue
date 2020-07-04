<template>
	<div id="Home">
		<Header/>
		<Main/>
		<Footer/>
	</div>
</template>

<script>
import Header from '../components/HeaderPart'
import Main from '../components/MainPart.vue'
import Footer from '../components/FooterPart.vue'

export default {
	name: 'home',
	
	components: {
		Header,
		Main,
		Footer
	}
}
</script>
