<script context="module">
	export const prerender = true;
</script>

<script lang="ts">
	const db = async () => {
		var response = await fetch('https://api.detzz.in.th/profile/');
		var result = await response.json();
		return result;
	}

	let call = db();

	let bdc:any;
	let age:any;
	let now:any = new Date();
	let yr:any = now.getFullYear();
</script>

<svelte:head>
	<title>About | Suphakit P.</title>
</svelte:head>

<section>
	{#await call}
		Loading..
	{:then dbs} 
		<div class="info">
			<div class="profile">
				<img src={dbs[0].proPic} alt="profile pic">
			</div>
			<div class="data">
				<h1>
					{dbs[0].name} {dbs[0].sName}
				</h1>
				
				<h3 class="subtext">
					{dbs[0].quote}
				</h3>
				
				<span style="display: none;">
					{bdc = new Date(1024074000000)}
				</span>

				<p>
					Birthday: {bdc.getFullYear()}, {bdc.getUTCDate() + 1} {bdc.toLocaleString('default', { month: 'long' })}
				</p>

				<p>
					Age: {yr - bdc.getFullYear()}
				</p>
			</div>
		</div>
	{/await}
</section>

<style>
	section {
		width: 80%;
		margin-left: auto;
		margin-right: auto;

		background-color: rgba(0, 0, 0, 0.4);
	}

	.info {
		display: flex;
		flex-direction: row;
	}

	.info .profile {
		width: 300px;
		height: auto;

		display: inline;
		padding: 1rem;
	}

	.info img {
		width: 100%;
		height: auto;

		border-radius: 50%;
	}

	.info .data {
		width: 100%;
		height: auto;

		display: inline;

		padding-left: 1rem;
	}

	.subtext {
		color: rgb(195, 195, 195);
	}

	@media only screen and (max-width: 700px) {
		.info {
			flex-direction: column;
			justify-content: center;
		}

		.info .profile {
			width: 100%;
			height: auto;

			display: inline;

			padding: 0;
			padding-top: 1rem;
			padding-bottom: 1rem;

			text-align: center;
			align-items: center;
			justify-content: center;
			
			margin-left: auto;
			margin-right: auto;
		}

		.info img {
			width: 300px;
			height: auto;

			border-radius: 50%;
		}

		.info .data {
			width: auto;
			height: auto;

			display: inline;

			padding-left: 1rem;
			padding-top: 1rem;
			padding-bottom: 1rem;
		}
	}
</style>
