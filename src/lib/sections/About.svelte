<script lang="ts">
	import calc from "../assets/calc_code.png";
	import login from "../assets/gold_login.png";

	const abouts = [
		{
			header: "How it Started",
			text: "For much of my life I've had an interest in computer technology, culminating in taking my high school's computer science class. Almost imediately, I was hooked. I loved the challenge of solving complex problems, using computers as a means to do so. Eventually, this lead me to enroll in Ball State's computer science program.",
			img: calc,
			caption:
				"A piece of code for a really simple spinning calculator I made while learning Javascript."
		},
		{
			header: "Where it's Going",
			text: "Since enrolling, I've joined Ball State's Digital Corps as a fullstack software developer. Here, I've learned necessary technical and nontechnical skills in which to design, build, and test applications of all kinds.",
			img: login
		}
	];
</script>

<section class=" main-site-section wrapper items-center gap-12 sm:flex">
	<h2 class=" main-site-header sm:vertical-text sm:border-b-0 sm:border-l-[0.75rem]">Who I Am</h2>

	<div class="w-full space-y-5">
		{#each abouts as about, index}
			<article
				class="w-full gap-5 sm:flex sm:*:w-1/2 {index % 2 === 1
					? 'sm:flex-row-reverse'
					: 'sm:flex-row'}"
			>
				<div class="">
					<img class="rounded-norm" src={about.img} alt="" />
					{#if about.caption}
						<p class=" text-[0.75rem] italic">{about.caption}</p>
					{/if}
				</div>
				<section>
					<h3 class="text-primary text-2xl font-black">{about.header}</h3>
					<p>{about.text}</p>
				</section>
			</article>
		{/each}
	</div>
</section>
