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
	<title>Suphakit P. | PUSSY is My Passsion</title>
</svelte:head>

<section>
	<div class="card">		
		{#await call}
			<div class="c-cont">
				Loading...
			</div>
		{:then dbs} 
			<div class="c-img">
				<img src={dbs[0].proPic} alt="loading" class="prof">
			</div>

			<div class="c-cont">
				<h2>
					{dbs[0].name} {dbs[0].sName}
				</h2>

				<span class="subtext">
					{dbs[0].quote}
				</span>
				<br />

				<div class="social-controller">
					<a href={dbs[0].footer[0].social[0].link}>
						<i class={dbs[0].footer[0].social[0].icon + ' fb bub'}></i>
					</a>
					<a href={dbs[0].footer[0].social[1].link}>
						<i class={dbs[0].footer[0].social[1].icon + ' tw bub'}></i>
					</a>
					<a href={dbs[0].footer[0].social[2].link}>
						<i class={dbs[0].footer[0].social[2].icon + ' gh bub'}></i>
					</a>
				</div>

				<div class="subtext" style="padding-top: 0.5rem; padding-bottom: 1rem;">
					<a href={mailto = "mailto:" + dbs[0].footer[0].mail}>
						{dbs[0].footer[0].mail}
					</a>
				</div>

				<a sveltekit:prefetch href="/donation">
					<button class="donation">
						Donation!
					</button>
				</a>
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

		margin-top: 1rem;
		margin-bottom: 1rem;
		margin-left: auto;
		margin-right: auto;

		padding: .5rem;
		padding-bottom: .3rem;
		border-radius: 1rem;
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

	.c-img {
		width: 80%;
		height: auto;
		background-color: rgb(201, 201, 201);
		border-radius: 50%;
		padding: 0.1rem !important;
		margin-left: auto !important;
		margin-right: auto !important;
		
		text-align: center;
		color: #2e2f2f;
	}

	.c-img img {
		width: 100%;
		height: 100%;
		border-radius: 50%;
		margin: auto;
	}

	.c-cont {
		width: 100% !important;
		color: #2e2f2f;
		background-color: whitesmoke;
		padding-top: 3rem;
		border-radius: 10px;
		text-align: center;
		margin-top: -3.3rem;
		/* padding-bottom: 2rem; */
	}

	.c-cont h2 {
		padding: 0.3rem;
		margin: 0;
	}

	.c-cont .subtext {
		color: grey;
		font-size: 14px;
	}

	.c-cont .subtext a {
		color: grey;
		font-size: 14px;
	}

	.c-cont .subtext a:hover {
		color: rgb(105, 104, 104);
		text-decoration: none;
	}

	.c-cont .social-controller {
		padding-top: 1rem;
		padding-bottom: 1rem;
	}

	.c-cont .social-controller a {
		text-decoration: none;
		height: auto;
	}

	.c-cont .social-controller a:hover {
		text-decoration: none;
		opacity: 0.6;
	}

	.c-cont .social-controller .bub{
		width: auto;
		height: auto;

		font-size: 30px;
		
		padding: .7rem;
		border-radius: 50%;
		margin-left: .5rem;
		margin-right: .5rem;
	}

	.c-cont .social-controller .fb.bub {
		background-color: #1876F3;
		color: whitesmoke;
	}
	.c-cont .social-controller .tw.bub {
		background-color: #1C9BF1;
		color: whitesmoke;
	}

	.c-cont .social-controller .gh.bub {
		background-color: #22272E;
		color: whitesmoke;
	}

	.c-cont .donation {
		width: 100%;
		height: auto;
		font-size: 1rem;
		
		background-color: #2e2f2f;
		color: whitesmoke;
		
		border: none;
		border-bottom-left-radius: 10px;
		border-bottom-right-radius: 10px;

		margin: 0;
		padding-top: 1rem;
		padding-bottom: 1rem;
	}

	.c-cont .donation:hover {
		opacity: 0.6;
	}
</style>