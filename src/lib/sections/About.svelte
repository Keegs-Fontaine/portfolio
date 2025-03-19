<script lang="ts">
	const abouts = [
		{
			header: 'How it Started',
			text: 'blah blah blah',
			img: 'https://picsum.photos/300/200'
		},
		{
			header: "Where it's Going",
			text: 'aah fdsjakl fdhsa fdsa',
			img: 'https://picsum.photos/300/200'
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
				<div class="rounded-norm overflow-clip">
					<img src={about.img} alt="" />
				</div>
				<section>
					<h3 class="text-primary text-2xl font-black">{about.header}</h3>
					<p>{about.text}</p>
				</section>
			</article>
		{/each}
	</div>
</section>
