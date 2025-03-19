<section class="main-site-section">
	<form class=" wrapper grid-cols-2 gap-5 space-y-10 md:grid">
		<h2 class="col-start-2 mb-12 md:text-right">
			<span class=" main-site-header">
				<span class="inline-block text-nowrap md:mb-10">Let's Work</span> Together
			</span>
		</h2>

		<section class="items-between row-start-1 flex flex-col justify-around space-y-5">
			<div class="flex flex-col">
				<label class="font-bold" for="name"> Name </label>
				<input class="rounded-norm bg-neutral-200 px-3 py-2" type="text" name="name" id="name" />
			</div>

			<div class="flex flex-col">
				<label class="font-bold" for="email"> Email </label>
				<input class="rounded-norm bg-neutral-200 px-3 py-2" type="email" name="email" id="email" />
			</div>
		</section>

		<div class="flex flex-col sm:col-span-2">
			<label class="font-bold" for="message"> How Can I Help? </label>
			<p class="italic">
				Send a brief description of the projects you’d like me to help bring to life.
			</p>
			<textarea
				rows={8}
				class="rounded-norm max-w-[70ch] bg-neutral-200 px-3 py-2"
				name="message"
				id="message"
			></textarea>
			<button type="submit" class=" btn-primary mt-5 w-fit"> Submit </button>
		</div>
	</form>
</section>
