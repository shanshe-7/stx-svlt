<script lang="ts">
	import type { Snippet } from 'svelte';

	let {
		name,
		fakeName = null,
		children
	}: {
		name: string;
		fakeName?: string | null;
		children: Snippet;
	} = $props();
</script>

<h1>hello: {name}</h1>
{@render children()}

<h2>{name.toLowerCase().replaceAll('sh', 'XX')}</h2>

{fakeName}

<style>
</style>
