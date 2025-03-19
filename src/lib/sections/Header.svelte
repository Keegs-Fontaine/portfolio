<script lang="ts">
	import logo from '$lib/assets/logo.svg';

	let isMenuOpen = $state(false);
</script>

<header
	class=" bg-primary-alpha max-sm:bg-primary fixed top-0 z-[100] w-full p-4 text-white backdrop-blur-xl"
>
	<nav class=" wrapper flex items-center justify-between font-bold">
		<a class="relative z-50" href="/">
			<img src={logo} alt="Keegan Fontaine" />
		</a>

		<ul
			class="max-sm:bg-primary flex justify-center gap-5 transition-transform max-sm:absolute max-sm:top-full max-sm:left-0 max-sm:w-screen max-sm:flex-col max-sm:text-center {isMenuOpen
				? ' max-sm:translate-y-[0]'
				: ' max-sm:translate-y-[-150%] '}"
		>
			<li>
				<a class=" block py-5" href="#projects">Projects</a>
			</li>
			<li>
				<a class=" block py-5" href="#about">About Me</a>
			</li>
			<li>
				<a class=" block py-5" href="#contact">Contact</a>
			</li>
		</ul>

		<button
			class="relative z-50 flex aspect-square w-12 flex-col justify-between *:block *:h-1/5 *:w-full *:bg-white sm:hidden"
			aria-label="Toggle menu"
			onclick={() => (isMenuOpen = !isMenuOpen)}
		>
			<span></span>
			<span></span>
			<span></span>
		</button>
	</nav>
</header>
