<script lang="ts">
	import { page } from '$app/stores';
</script>

<header>
	<nav>
		<ul>
			<a sveltekit:prefetch href="/">
				<li>
					home
				</li>
			</a>

			<li></li>

			<a sveltekit:prefetch href="https://blog.suphakit.net">
				<li>
					blog
				</li>
			</a>

			<li></li>

			<a sveltekit:prefetch href="/about">
				<li class:active={$page.url.pathname === '/about'}>
					about
				</li>
			</a>

			<li></li>
		</ul>
	</nav>
</header>

<style>
	nav {
		width: 100%;
		height: auto;
	}

	ul {
		margin: 0;
		padding: 0;
		background-color: whitesmoke;
		color: #2e2f2f;
		text-align: right;
		padding-top: 1rem;
		padding-bottom: 1rem;
	}

	li {
		display: inline;
		padding: .5rem;
		padding-top: 1rem;
		padding-bottom: 1rem;
		background-color: whitesmoke;
	}

	a li:hover {
		background-color: rgb(182, 182, 182);
	}
</style>
