<script lang="ts">
	import Header from './Header.svelte';
	let name = $state('Shanshe');

	let status: 'OPEN' | 'CLOSED' = $state('OPEN');

	let fullName = $derived(`${name} Kenkadze`);

	function onclick() {
		return (status = status === 'OPEN' ? 'CLOSED' : 'OPEN');
	}
</script>

<Header {name} fakeName="Mao">
	<h3>effort</h3>
</Header>

<h2>
	{fullName}
</h2>

<input type="text" bind:value={name} />

<p>The store now is {status}</p>
<button {onclick}> Toggle status</button>
