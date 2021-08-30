<script>
	import { createEventDispatcher } from 'svelte';
	let title = '';
	const dispatch = createEventDispatcher();

	const add = () => {
		dispatch('addTodo', title);
	};
</script>

<input type="text" bind:value={title} />
<button on:click={add}>Add todo</button>
