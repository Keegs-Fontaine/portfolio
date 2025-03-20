<script lang="ts">
	import chevron from "$lib/assets/icons/chevron.svg";
	import { fade } from "svelte/transition";

	import gold from "../assets/gold.png";
	import ha from "../assets/ha.png";

	type Project = {
		img: string;
		title: string;
		text: string;
		tech: string[];
		links: { [key: string]: string };
	};

	const projects: Project[] = [
		{
			img: ha,
			title: "Humanizing Addiction",
			text: "A public website for an immersive learning class at Ball State, meant to fight the negative stigma surrounding drug addiction in the Muncie community. One of this project's unique challenges was allowing complete content management for the students of the immersive learning class -- leading to the use of Wordpress as a headless CMS, in which our clients would supply page content with a simultaneous design and development cycle. ",
			tech: ["React", "Typescript", "Wordpress/PHP"],
			links: { "Live Site": "http://humanizing-addiction.s3-website-us-east-1.amazonaws.com" }
		},
		{
			img: gold,
			title: "BSU's Gold Program",
			text: "A website to advertise Ball State's GOLD program across campus, an opportunity for graduate students to engage with their community to a greater extent, and learn necessary industry skills. With a need to track user progress through the program, this site integrates with Ball State's SSO authentication to allow for a customized profile page, with an admin panel to manage. ",
			tech: ["Sveltekit", "Typescript", "AdonisJS", "Docker/containerization", "MySQL"],
			links: { "Live Site": "https://gold.apsoprojects.org" }
		}
	];

	const moveLeft = () => {
		if (currentProject > 0) {
			currentProject--;
		} else {
			currentProject = projects.length - 1;
		}
	};

	const moveRight = () => {
		if (currentProject < projects.length - 1) {
			currentProject++;
		} else {
			currentProject = 0;
		}
	};

	let currentProject = $state(0);
	let isAnimating = $state(false);

	const dot = " block aspect-square w-5 rounded-full bg-white";
</script>

<section class="main-site-section space-bg">
	<div class="wrapper">
		<h2 class="main-site-header">My Projects</h2>

		<section
			class=" rounded-norm outline-neutral-dark relative w-full overflow-clip bg-white outline-2 outline-offset-[-1px]"
		>
			{#each [projects[currentProject]] as project (currentProject)}
				<article
					transition:fade
					onintrostartcapture={() => (isAnimating = true)}
					onintroend={() => (isAnimating = false)}
					class=" project-card mx-auto flex w-full flex-col items-stretch gap-4 transition-all sm:flex-row sm:*:w-1/2 {isAnimating
						? 'absolute'
						: ''}"
				>
					<div>
						<img loading="lazy" src={project.img} alt="" />
					</div>
					<div class=" text-neutral-dark flex flex-col gap-5 p-5 text-lg font-bold">
						<h3 class=" text-primary text-2xl font-black md:text-5xl">{project.title}</h3>
						<p class=" font-light">{project.text}</p>
						<div class="mt-auto">
							<span class=" text-primary">Some of the tech:</span>
							{#each project.tech as tech, index}
								<span>{tech}{index === project.tech.length - 1 ? "" : ", "} </span>
							{/each}
						</div>
						<div class=" flex gap-5">
							{#each Object.entries(project.links) as [linkName, linkValue]}
								<a href={linkValue} target="_blank" class="btn-primary">{linkName}</a>
							{/each}
						</div>
					</div>
				</article>
			{/each}
		</section>

		<div class=" mt-5 flex items-center justify-center gap-4">
			<button disabled={isAnimating} onclick={moveLeft}>
				<img class=" rotate-180" src={chevron} alt="" />
			</button>

			{#each projects as _, index}
				{#if index === currentProject}
					<span class={dot + " border-primary border-4"}></span>
				{:else}
					<span class={dot}></span>
				{/if}
			{/each}

			<button disabled={isAnimating} onclick={moveRight}><img src={chevron} alt="" /></button>
		</div>
	</div>
</section>

<style>
	.space-bg {
		background-position-x: -10rem;
		background-position-y: calc(100% + 10rem);
	}
</style>
