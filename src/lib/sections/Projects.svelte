<script lang="ts">
	import chevron from "$lib/assets/icons/chevron.svg";
	import { fade } from "svelte/transition";

	import ha from "../assets/ha.png";
	import orchid from "../assets/orchid_db.png";
	import ceres from "../assets/ceres.png";
	import mybsu from "../assets/mybsu.png";
	import { onMount } from "svelte";

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
			img: orchid,
			title: "BSU Orchid Greenhouse",
			text: "Ball State's Orchid Greenhouse houses thousands of separate orchid flowers for view by both the general public and academia. This was a huge project that involved the development of a public facing website to view the plant collection, an admin panel with which to update and manage plant data, and new strategies to systematically migrate thousands of plants to a newly developed database.",
			tech: ["Svelte", "Typescript", "AdonisJS/MVC Architecture", "MySQL", "Docker"],
			links: {}
		},
		{
			img: ceres,
			title: "CERES",
			text: "A website for Ball State's Center for Energy Research Education Service (CERES), cateloguing the history and goals of the organiztion to study energy use and conservation. This site is filled with fun little animations, and was one of my first experiences getting thrown into a codebase halfway to completion. It was an incredibly valuable experience!",
			tech: ["React", "Typescript", "React Router", "GSAP"],
			links: { "Live Site": "http://cap-ceres.s3-website.us-east-2.amazonaws.com" }
		},
		{
			img: mybsu,
			title: "MyBallState",
			text: "A huge project, 'MyBallState' is BSU's new student information portal. The site functions as a centerpoint for a collection of widgets, for which I was part of the development process. Because each widget requirs its own design and functionality, the design and development process was intensely iterative -- and constantly engaging.",
			tech: ["HTML/CSS/JS", "Asynchronous Data Fetching", "RSS Feeds"],
			links: { "Live Site": "https://myballstate.bsu.edu/public/dashboard" }
		}
	];

	let currentProject = $state(0);

	const dot = " block aspect-square w-5 rounded-full bg-white";

	function getNextProj() {
		return currentProject >= projects.length - 1 ? 0 : currentProject + 1;
	}
	function getLastProj() {
		return currentProject <= 0 ? projects.length - 1 : currentProject - 1;
	}

	let carouselElements: HTMLElement[] = $state([]);

	let currentScrollPos = $state(0);
</script>

<section class="main-site-section space-bg">
	<div class="wrapper">
		<h2 class="main-site-header">My Projects</h2>

		<div class=" overflow-auto rounded-2xl">
			<section
				onscrollend={(e) => {
					// currentProject = e.currentTarget.scrollLeft / e.currentTarget.clientWidth;
				}}
				class=" rounded-norm outline-neutral-dark custom-scrollbar relative flex w-full snap-x snap-mandatory overflow-x-hidden bg-white outline-2 outline-offset-[-1px]"
			>
				{#each projects as project, i}
					<article
						bind:this={carouselElements[i]}
						class=" project-card transition-height mx-auto flex h-fit w-full shrink-0 snap-center flex-col items-stretch gap-4 transition-all lg:flex-row lg:*:w-1/2"
					>
						<div class=" grid overflow-y-clip md:h-[30rem]">
							<img src={project.img} alt="" />
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
		</div>

		<div class=" mt-5 flex items-center justify-center gap-4">
			<button
				onclick={() => {
					currentProject = getLastProj();

					carouselElements[currentProject].scrollIntoView({
						inline: "center",
						block: "center",
						behavior: "smooth"
					});
				}}
			>
				<img class=" rotate-180" src={chevron} alt="Previous" />
			</button>

			{#each projects as _, index}
				{#if index === currentProject}
					<span class={dot + " border-primary border-4"}></span>
				{:else}
					<span class={dot}></span>
				{/if}
			{/each}

			<button
				onclick={() => {
					currentProject = getNextProj();

					carouselElements[currentProject].scrollIntoView({
						inline: "center",
						block: "center",
						behavior: "smooth"
					});
				}}><img src={chevron} alt="Next" /></button
			>
		</div>
	</div>
</section>

<style>
	.space-bg {
		background-position-x: -10rem;
		background-position-y: calc(100% + 10rem);
	}

	.custom-scrollbar {
		scrollbar-color: var(--color-primary) gray;
	}
</style>
