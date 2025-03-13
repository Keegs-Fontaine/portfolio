<script lang="ts">
	import '../app.css';
	let { children } = $props();
</script>

<svelte:head>
	<title>Keegan Fontaine</title>
</svelte:head>

{@render children()}
