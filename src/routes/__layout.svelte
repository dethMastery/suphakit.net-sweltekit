<script lang="ts">
	import Header from '$lib/header/Header.svelte';
	import '../main.css';
</script>


<main>
	<Header />

	<slot />
</main>

<style>
	main {
		width: 100%;
		min-height: 100vh;
		height: auto;
		background-color: rgba(0, 0, 0, 0.4);
		color: whitesmoke;
	}
</style>
