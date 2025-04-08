<script lang="ts">
	import { fly } from 'svelte/transition';

	const QUESTIONS = [
		{
			question: 'What is your name',
			id: 'name',
			type: 'text'
		},
		{
			question: 'What is your bday',
			id: 'birthday',
			type: 'date'
		},
		{
			question: 'What is your favorite color',
			id: 'color',
			type: 'color'
		}
	];

	let formState = $state({
		answers: {},
		step: 0,
		error: ''
	});

	function handleNextStep(id: string) {
		if (!formState.answers[id]) {
			formState.error = 'Please fill out the form input';
			return;
		}

		formState.step += 1;
		formState.error = '';
	}

	$effect(() => {
		console.log('Mounted');

		return () => {
			console.log('On mounted');
		};
	});

	$effect(() => {
		console.log('formstep', formState);
	});
</script>

<h1>This is a form</h1>

<main>
	{#if formState.step >= QUESTIONS.length}
		<p>Thank you</p>
	{:else}
		<span>Step: {formState.step + 1}</span>
	{/if}

	{#each QUESTIONS as { id, question, type }, idx (id)}
		{#if formState.step == idx}
			<div
				in:fly={{ x: 400, duration: 400, opacity: 0, delay: 400 }}
				out:fly={{ x: -400, duration: 400, opacity: 0 }}
			>
				{@render formStep({ question, id, type })}
			</div>
		{/if}
	{/each}

	{#if formState.error}
		<p class="error">{formState.error}</p>
	{/if}
</main>

{#snippet formStep({ question, id, type }: { type: string; id: string; question: string })}
	<article>
		<div>
			<label for={id}>{question}</label>
			<input {type} {id} bind:value={formState.answers[id]} />
		</div>
		<button onclick={() => handleNextStep(id)}>Next</button>
	</article>
{/snippet}

<style>
	.error {
		width: fit-content;
		padding: 2px;
		color: brown;
	}
</style>
