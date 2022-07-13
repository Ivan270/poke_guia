<template>
	<div>
		<div id="blur-container"></div>
		<div class="container">
			<h1>Pokeguía: Busca un Pokemon</h1>
			<div id="form-container">
				<form action="">
					<label for="">Nombre del Pokemon</label>
					<input
						type="text"
						placeholder="Nombre del Pokemon"
						v-model="pokemon.name"
					/>
					<button type="submit" @click.prevent="pokeFind">Buscar</button>
				</form>
			</div>

			<div id="resultado">
				<h3 id="nombre">
					Nombre: <span>{{ pokemon.name }}</span>
				</h3>
				<img :src="img" alt="" width="150px" />
				<div id="habilidades">
					<h3>Habilidades:</h3>
					<p v-for="ability in pokeAbilities" :key="ability">{{ ability }}</p>
				</div>

				<div id="movimientos">
					<h3>Movimientos:</h3>
					<ol>
						<li v-for="move in pokeMoves" :key="move">{{ move }}</li>
					</ol>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'poke-guia',
		// props: {},
		data: function () {
			return {
				pokemon: {
					name: 'pikachu',
					image: '',
					abilities: [],
					moves: [],
					sprites: { front_default: '' },
				},
			};
		},
		computed: {
			// foto
			img() {
				// console.log(this.pokemon.sprites.front_default);
				return this.pokemon.sprites.front_default;
			},
			// movimientos
			pokeMoves() {
				let a = this.pokemon.moves;
				function getMoves(item) {
					let b = item.move.name;
					return b;
				}
				return a.map(getMoves);
			},
			// habilidades
			pokeAbilities() {
				let arr = this.pokemon.abilities;
				function getAbilities(item) {
					let arr2 = item.ability.name;
					// console.log(arr2);
					return arr2;
				}
				let arrFinal = arr.map(getAbilities);
				console.log(arrFinal);
				return arrFinal;
			},
		},
		methods: {
			async pokeFind() {
				try {
					let response = await fetch(
						`https://pokeapi.co/api/v2/pokemon/${this.pokemon.name}`
					);
					if (!response.ok) throw 'Error en petición';
					let json = await response.json();
					// console.log(json);
					this.pokemon = json;
				} catch (error) {
					console.log(error);
				}
			},
		},
		// watch: {},
		// components: {},
		// mixins: [],
		// filters: {},
		// -- Lifecycle Methods
		created() {
			this.pokeFind();
		},
		// -- End Lifecycle Methods
	};
</script>

<style scoped>
	#blur-container {
		height: 100vh;
		place-content: center;
		background: black;
		background-image: url('/src/assets/pokemon-bg.jpg');
		filter: blur(4px);
	}
	.container {
		display: grid;
		/* grid-gap: 15px; */
		place-content: center;
		grid-template-columns: repeat(6, 1fr);
		grid-template-rows: 1fr, 1fr, 1fr;
		background-color: rgb(0, 0, 0); /* Fallback color */
		background-color: rgba(0, 0, 0, 0.4); /* Black w/opacity/see-through */
		border: 2px solid #f1f1f1;
		color: white;
		font-weight: bold;
		border-radius: 10px;
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		z-index: 2;
		height: 350px;
		width: 80%;
		padding: 20px;
	}
	h1 {
		grid-column: 1 / 4;
		grid-row: 1/2;
		font-weight: 500;
		letter-spacing: 3px;
		padding: 20px 0px 0px 0px;
	}
	h3 {
		font-weight: 500;
	}
	#form-container {
		align-self: center;
		grid-column: 1 / 4;
		grid-row: 2/3;
	}
	form {
		padding-bottom: 20px;
	}

	label {
		font-weight: 400;
		letter-spacing: 3px;
		font-size: 25px;
	}
	input {
		padding-left: 5px;
		height: 30px;
		margin: 0px 20px;
		background: none;
		border: 2px solid white;
		border-radius: 5px;
		color: white;
		outline: none;
	}
	::placeholder {
		color: #ecd0f4;
	}
	button {
		width: 80px;
		height: 30px;
		background: none;
		border: 2px solid #8dcce2;
		border-radius: 8px;
		color: #8dcce2;
		cursor: pointer;
		transition: 0.3s;
	}
	button:hover {
		background: #ecd0f4;
		color: white;
		border-color: #ecd0f4;
	}
	button:active {
		width: 75px;
		height: 25px;
	}
	#resultado {
		grid-column: 4 / 7;
		grid-row: 1/3;
		display: grid;
		grid-template-columns: repeat(6, 1fr);
	}
	#resultado h1 {
		grid-column: 4/7;
		grid-row: 1/2;
	}
	#nombre {
		align-self: center;
		text-transform: capitalize;
		grid-column: 1/3;
	}
	#nombre span {
		font-weight: 200;
		font-size: 25px;
	}
	#resultado img {
		grid-column: 1/2;
		grid-row: 2/4;
	}
	#habilidades {
		font-size: 18px;
		text-transform: capitalize;
		grid-column: 3/5;
		grid-row: 1/4;
	}
	#habilidades p {
		font-weight: 200;
	}
	#movimientos {
		grid-column: 5/7;
		grid-row: 1/4;
		font-weight: 200;
		height: 200px;
		width: 300px;
		list-style-position: inside;
		overflow-y: scroll;
	}
	#movimientos::-webkit-scrollbar {
		width: 10px;
	}
	#movimientos::-webkit-scrollbar-track {
		box-shadow: inset 0 0 5px #356699;
		border-radius: 10px;
	}
	#movimientos::-webkit-scrollbar-thumb {
		background: #ecd0f4;
		border-radius: 10px;
	}
	#movimientos::-webkit-scrollbar-thumb:hover {
		background: #356699;
	}
</style>
