<script lang="ts">
	import chevron from '$lib/assets/icons/chevron.svg';
	import { fade } from 'svelte/transition';

	type Project = {
		img: string;
		title: string;
		text: string;
		links: { [key: string]: string };
	};

	const projects: Project[] = [
		{
			img: 'https://picsum.photos/300/300',
			title: 'Some cool project title',
			text: 'lorem ipsum solar domit f dsa fdh fdsaj h ljk fdjsakl fhdsgasad ',
			links: { github: '', live: '' }
		},
		{
			img: 'https://picsum.photos/300/300',
			title: 'Some cool as df title',
			text: 'lorem ipsum solar domit f dsa fdh fdsaj h ljk fdjsakl fhdsgasad ',
			links: { github: '', live: '' }
		},
		{
			img: 'https://picsum.photos/300/300',
			title: ' fdsatle',
			text: 'lorem ipsum solar domit f dsa fdh fdsaj h ljk fdjsakl fhdsgasad ',
			links: { github: '', live: '' }
		},
		{
			img: 'https://picsum.photos/300/300',
			title: 'Some cool  fdsoapu8y7tdfjksnalm;o fipdusoigay title',
			text: 'lorem ipsum solar domit f dsa fdh fdsaj h ljk fdjsakl fhdsgasad ',
			links: { github: '', live: '' }
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

	const dot = ' block aspect-square w-5 rounded-full bg-white';
</script>

<section class="main-site-section space-bg">
	<div class="wrapper">
		<h2 class="main-site-header">My Projects</h2>

		<section class=" rounded-norm relative w-full overflow-clip bg-white">
			{#each [projects[currentProject]] as project (currentProject)}
				<article
					transition:fade
					onintrostartcapture={() => (isAnimating = true)}
					onintroend={() => (isAnimating = false)}
					class=" project-card mx-auto flex flex-col items-stretch gap-4 sm:flex-row sm:*:w-1/2 {isAnimating
						? 'absolute'
						: ''}"
				>
					<div>
						<img class="h-full" src={project.img} alt="" />
					</div>
					<div class=" text-neutral-dark flex flex-col justify-between gap-4 py-12">
						<h3 class=" text-primary text-5xl font-black">{project.title}</h3>
						<p>{project.text}</p>
						<div class="flex gap-5">
							{#each Object.entries(project.links) as [linkName, linkValue]}
								<a href={linkValue} class="btn-primary">{linkName}</a>
							{/each}
							<a href={project.links.live} class="btn-primary">Live</a>
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
					<span class={dot + ' border-primary border-4'}></span>
				{:else}
					<span class={dot}></span>
				{/if}
			{/each}

			<button disabled={isAnimating} onclick={moveRight}><img src={chevron} alt="" /></button>
		</div>
	</div>
</section>

<style>
	.is-animating {
		position: absolute;
		background-color: blue !important;
		scale: 0.2;
	}
</style>
