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
					About
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
					Skill
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
	{/await}
</section>

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
