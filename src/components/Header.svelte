<script>
	import { getContext, setContext } from 'svelte';
	import TasksCount from './TasksCount.svelte';

	export let counter = {};
</script>

<div class="header">
	<h1>Tasks</h1>

	<TasksCount bind:counter />
</div>

<style>
	.header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 4rem;
	}

	.header h1 {
		font-size: 1.8rem;
		color: var(--primary-clr);
		font-weight: var(--fw-bold);
	}
</style>
