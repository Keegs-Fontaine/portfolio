<script>
	import About from '$lib/sections/About.svelte';
	import Contact from '$lib/sections/Contact.svelte';
	import Footer from '$lib/sections/Footer.svelte';
	import Header from '$lib/sections/Header.svelte';
	import Hero from '$lib/sections/Hero.svelte';
	import Projects from '$lib/sections/Projects.svelte';
</script>

<Header />
<Hero />
<div id="about">
	<About />
</div>
<div id="projects">
	<Projects />
</div>
<div id="contact">
	<Contact />
</div>
<Footer />
