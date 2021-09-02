<script>
	import { createEventDispatcher } from 'svelte';
	export let title = '';
	const dispatch = createEventDispatcher();

	$: isTitleUndefined = title === '' ? true : false;

	const add = () => {
		dispatch('addTodo', title);
	};
</script>

<div class="form-block">
	<input type="text" bind:value={title} />
	<button disabled={isTitleUndefined} on:click={add}> Add todo</button>
</div>

<style>
	.form-block {
		width: 100%;
		display: flex;
		margin-bottom: 2rem;
		align-items: stretch;
		justify-content: center;
	}

	input {
		flex: 1;
		padding: 1rem 2rem;
		font-size: 1.5rem;
		outline: none;
	}

	input:focus {
		border: 1px solid var(--primary-clr);
	}

	button {
		cursor: pointer;
		background-color: var(--primary-clr);
		color: #fff;
		font-size: 1.5rem;
		text-transform: uppercase;
		padding: 1rem 2.5rem;
		transition: opacity 0.2s;
	}

	button:hover {
		opacity: 0.75;
	}

	button:disabled {
		background-color: #999;
		pointer-events: none;
	}
</style>
