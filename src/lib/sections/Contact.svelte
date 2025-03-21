<script lang="ts">
	import { PUBLIC_FORMS_URL } from "$env/static/public";

	let form: HTMLFormElement;

	const handleFormSubmission = async (e: Event) => {
		e.preventDefault();

		const formData = new FormData(form);

		await fetch(PUBLIC_FORMS_URL, {
			method: "POST",
			body: formData,
			headers: {
				Accept: "application/json"
			}
		});
	};

	let submission: "uninitialized" | "pending" | "complete" | "error" = "uninitialized";
</script>

<section class="main-site-section">
	<form
		bind:this={form}
		onsubmit={(e) => {
			submission = "pending";
			handleFormSubmission(e)
				.then(() => (submission = "complete"))
				.catch(() => (submission = "error"));
		}}
		class=" wrapper grid-cols-2 gap-5 space-y-20 md:grid"
	>
		<section class="col-start-2 mb-12 space-y-10 md:text-right">
			<h2>
				<span class=" main-site-header">
					<span class="mb-8 inline-block text-nowrap md:mb-10">Let's Work</span> Together
				</span>
			</h2>
			<p class=" italic">
				Or email me directly at <a class="text-primary" href="mailto:keegsfontaine@gmail.com"
					>keegsfontaine@gmail.com</a
				>
			</p>
		</section>

		{#if submission === "uninitialized" || submission === "pending"}
			<section class="items-between row-start-1 flex flex-col justify-around space-y-5">
				<div class="flex flex-col">
					<label class="font-bold" for="name"> Name </label>
					<input
						disabled={submission === "pending"}
						required
						class="rounded-norm bg-neutral-200 px-3 py-2"
						type="text"
						name="name"
						id="name"
					/>
				</div>

				<div class="flex flex-col">
					<label class="font-bold" for="email"> Email </label>
					<input
						disabled={submission === "pending"}
						required
						class="rounded-norm bg-neutral-200 px-3 py-2"
						type="email"
						name="email"
						id="email"
					/>
				</div>
			</section>

			<div class="flex flex-col sm:col-span-2">
				<label class="font-bold" for="message"> How Can I Help? </label>
				<p class="italic">
					Send a brief description of the projects you’d like me to help bring to life.
				</p>
				<textarea
					disabled={submission === "pending"}
					required
					rows={8}
					class="rounded-norm focus-within:outline-primary max-w-[70ch] resize-none bg-neutral-200 px-3 py-2"
					name="message"
					id="message"
				></textarea>
				<button disabled={submission === "pending"} type="submit" class=" btn-primary mt-5 w-fit">
					Submit
				</button>
			</div>
		{:else if submission === "complete"}
			<div class=" row-start-1">
				<h1 class="text-primary text-5xl font-black">Thanks!</h1>
				<p class=" text-xl font-bold">
					Your message has been sent, I'll get back as soon as I can!
				</p>
			</div>
		{:else if submission === "error"}
			<div class=" row-start-1">
				<h1 class="text-primary text-5xl font-black">Oops!</h1>
				<p class=" text-xl font-bold">
					Sorry! We couldn't process your message right now. Try again later (or email me directly
					at <a class="text-primary" href="mailto:keegsfontaine@gmail.com">
						keegsfontaine@gmail.com
					</a>
					)
				</p>
			</div>
		{/if}
	</form>
</section>
