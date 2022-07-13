<template>
	<div id="app">
		<poke-guia></poke-guia>
	</div>
</template>

<script>
	import Pokeguia from '@/components/Pokeguia.vue';
	export default {
		name: 'App',
		data() {
			return {
				//  capturar(){
				//  }
			};
		},
		components: {
			'poke-guia': Pokeguia,
		},
	};
</script>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@200;400;500&display=swap');
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}
	#app {
		font-family: 'Oswald', sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		color: #2c3e50;
		height: 100vh;
	}
</style>
