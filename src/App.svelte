<main>
	<h1>Hola {name}!</h1>
	<Menu/>
	<p>Hecho con ❤</p>
</main>

<script>
	import Menu from "./Menu.svelte"
	export let name;
</script>

<style>
	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
	}
	
	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 9002;
		font-weight: 100;
		margin-bottom: 10px;
		padding: 30px;
	}

	@media (max-width: 640px) {
		main {
			text-align: center;
			max-width: 100%;
			margin: 0;
		}
		h1 {
			text-align: left;
		}
	}
</style>