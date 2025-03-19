<script lang="ts">
	import logo from '$lib/assets/logo.svg';
	import Linkedin from '$lib/assets/icons/linkedin.svelte';
	import Github from '$lib/assets/icons/github.svelte';
	import Resume from '$lib/assets/icons/resume.svelte';
	import type { Snippet } from 'svelte';

	const links = [
		{
			name: 'LinkedIn',
			icon: Linkedin,
			link: ''
		},
		{
			name: 'GitHub',
			icon: Github,
			link: ''
		},
		{
			name: 'Resume',
			icon: Resume,
			link: ''
		}
	];
</script>

<footer class="bg-primary w-screen p-4">
	<nav class="wrapper flex flex-col items-center sm:flex-row sm:justify-between">
		<a class=" relative z-50 max-w-[3rem]" href="/">
			<img src={logo} alt="Keegan Fontaine" />
		</a>

		<ul class="flex flex-wrap items-center justify-center gap-5 pt-5">
			{#each links as link}
				<li>
					<a
						class="flex gap-1 text-white *:stroke-white"
						href={link.link}
						target="_blank"
						rel="noopener noreferrer"
					>
						<link.icon />
						<span>{link.name}</span>
					</a>
				</li>
			{/each}
		</ul>
	</nav>
</footer>
