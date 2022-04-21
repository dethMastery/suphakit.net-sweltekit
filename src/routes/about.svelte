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
		<center>
			Loading..
		</center>
	{:then dbs} 
		<div class="head-class info" id="info">
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

		<div class="head-class about" id="about">
			<h1>
				<u>
					About;
				</u>
			</h1>
			
			<h2 style="padding-left: 1rem;">
				{dbs[0].desc}
			</h2>

			<p style="padding-left: 2rem;">
				{dbs[0].subDesc}
			</p>

			<h2>
				<u>
					Education Profile
				</u>
			</h2>
			<ul style="padding-left: 3rem;">
				{#each dbs[0].Education.reverse() as edu}
					<li style="padding-bottom: 1rem;">
						[{edu.year}] {edu.grade} {edu.school}
					</li>
				{/each}
			</ul>
		</div>

		<div class="head-class skill" id="skill">
			<h1>
				<u>
					Skill;
				</u>
			</h1>

			<div class="skill-holder">
				{#each dbs[0].skill as skl}
					<div class="skl-card">
						<div class="skl-img">
							<img src={skl.path} alt={skl.name}>
						</div>
						<br>
						<div class="skl.data">
							<span>
								<b>
									{skl.name}
								</b>
							</span>
							<br>
							<span>
								{skl.duration}
							</span>
						</div>
					</div>
				{/each}
			</div>
		</div>

		<div class="head-class featured" id="featured">
			<h1>
				<u>
					Featured Repository;
				</u>
			</h1>

			<div class="repo-holder">
				{#each dbs[0].fRepo as repo}
					<div class="repo-card">
						<div class="repo-head">
							<h1>
								<u>
									{repo.name}
								</u>
								{#if repo.lang != ''}
									&#183;
									<span class="lang">
										{repo.lang}
									</span>
								{/if}
							</h1>
						</div>
						<div class="repo-cont">
							<span>
								{repo.desp}
							</span>
						</div>
						<div class="repo-info">
							<a sveltekit:prefetch href={repo.link}>
								<button class="repo-button">
									Repository Link >
								</button>
							</a>
						</div>
					</div>
				{/each}
			</div>
		</div>
	{/await}
</section>

{#await call}
	<span></span>
{:then dbs} 
	<div class="footer">
		&copy; Copyright 2022 <a sveltekit:prefetch href="https://suphakit.net">Suphakit P.</a>
	</div>
{/await}

<style>
	section {
		width: 80%;
		margin-left: auto;
		margin-right: auto;

		background-color: rgba(0, 0, 0, 0.4);
	}

	.head-class {
		width: auto;
		height: auto;

		padding: 1rem;
		padding-top: 0;
		padding-bottom: 0;

		margin-bottom: 1rem;
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

	.skill .skill-holder {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		gap: 1rem;
		justify-content: center;
		padding-bottom: 1rem;
	}

	.skill .skl-card {
		width: 10rem;
		background-color: whitesmoke;
		color: #2e2f2f;
		padding: 1rem;
		border-radius: 10px;
		text-align: center;
	}

	.skill .skl-card .skl-img {
		width: 100px;
		height: 100px;

		margin-left: auto;
		margin-right: auto;
	}

	.skill .skl-card .skl-img img {
		width: 100px;
		height: 100px;
	}

	.featured .repo-holder {
		display: flex;
		flex-direction: row;
		justify-content: center;
		flex-wrap: wrap;
		gap: 1rem;
		padding-bottom: 1rem;
	}

	.featured .repo-holder .repo-card {
		background-color: whitesmoke;
		color: #2e2f2f;
		border-radius: 10px;
		width: 20rem;
	}

	.featured .repo-holder .repo-card .repo-head {
		width: auto;
		height: auto;

		padding-left: 1rem;
		padding-right: 1rem;
	}

	.featured .repo-holder .repo-card .repo-head .lang {
		font-size: 15px;
		color: grey;
	}

	.featured .repo-holder .repo-card .repo-cont {
		width: auto;
		height: 5rem;
		padding-left: 2rem;
		padding-right: 2rem;
	}

	.featured .repo-holder .repo-card .repo-info {
		width: 100%;
	}

	.featured .repo-holder .repo-card .repo-info .repo-button {
		border: none;
		border-bottom-right-radius: 10px;
		border-bottom-left-radius: 10px;

		background-color: #2e2f2f;
		color: whitesmoke;

		width: 100%;
		height: 100%;

		padding-top: 1rem;
		padding-bottom: 1rem;

		cursor: pointer;
	}

	.featured .repo-holder .repo-card .repo-info .repo-button:hover {
		opacity: 0.6;
	}

	.footer {
		width: 100%;
		background-color: whitesmoke;
		color: #2e2f2f;
		text-align: center;
		padding-top: 1rem;
		padding-bottom: 1rem;
	}

	.footer a {
		color: #2e2f2f;
		text-decoration: none;
	}

	.footer a:hover {
		color: #2e2f2f;
		text-decoration: underline;
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
