<script context="module" lang="ts">
	export const prerender = true;
</script>

<script lang="ts">
	const db = async () => {
		var response = await fetch('https://api.detzz.in.th/profile/');
		var result = await response.json();
		return result;
	}

	let call = db();
	let mailto;
</script>


<svelte:head>
	<title>Donation | Suphakit P.</title>
</svelte:head>

<section>
	<div class="card">		
		{#await call}
			<div class="c-cont">
				Loading...
			</div>
		{:then dbs} 
			<div class="c-cont">
                <h1>
                    <u>
                        Donation
                    </u>
                </h1>
                
				{#each dbs[0].payment as pm}
                    <p>
                        {pm.name} : {pm.target}
                    </p>
                {/each}
                <br>
                <p>
                    {dbs[0].payment[0].uName}
                </p>
			</div>
		{/await}
	</div>

	<div class="logo">
		<a href="https://suphakit.net">
			<img src="logo.png" alt="Logo">
		</a>
	</div>
</section>

<style>
	section {
		width: 100%;
	}

	.logo {
		background-color: whitesmoke;
		width: 10%;
		height: auto;

		/* margin-top: 1rem; */
		/* margin-bottom: 1rem; */
		margin-left: auto;
		margin-right: auto;

		padding: .5rem;
		padding-bottom: .3rem;
		border-radius: 1rem;

		margin-top: -1rem;
	}

	.logo img {
		width: 100%;
		height: auto;
	}

	.card {
		width: 18rem;
		height: auto;
		margin-left: auto;
		margin-right: auto;
		margin-top: 2rem;
	}

	.c-cont {
		width: 100% !important;
		color: #2e2f2f;
		background-color: whitesmoke;
        padding-top: 1rem;
		border-radius: 10px;
		text-align: center;
		padding-bottom: 1rem;
	}

    .c-cont h1 {
		padding: 0.3rem;
		margin: 0;
	}
</style>