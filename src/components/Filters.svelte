<script>
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

	const sort = () => {
		dispatch('sortTodos', sortDirection);
	};

	export let view = 'all';
	export let sortDirection = 2;
</script>

<div class="filters">
	<div class="filters-item">
		<label for="all">all </label>
		<input type="radio" id="all" bind:group={view} value="all" />
	</div>

	<div class="filters-item">
		<label for="active">Active</label>
		<input type="radio" id="active" bind:group={view} value="active" />
	</div>

	<div class="filters-item">
		<label for="completed">completed</label>
		<input type="radio" id="completed" bind:group={view} value="completed" />
	</div>

	<div class="filters-item filters-right">
		<span class="fliters-sort" on:click={sort}>
			{#if sortDirection === 1}
				<i class="fi-rr-angle-up" />
			{:else if sortDirection === 2}
				<i class="fi-rr-angle-down" />
			{/if}

			<span>sort {sortDirection === 1 ? 'up' : 'down'}</span>
		</span>
	</div>
</div>

<style>
	.filters {
		display: flex;
		font-size: 1.2rem;
		align-items: center;
		width: 100%;
	}

	.filters-item {
		display: flex;
		align-items: center;
	}

	.filters-item:not(:last-child) {
		margin-right: 1.5rem;
	}

	.filters-item label {
		order: 1;
		margin-left: 0.5rem;
	}

	.mr-1 {
		margin-right: 0.5rem;
	}

	.filters-right {
		justify-self: flex-end;
		display: inline-block;
		margin-left: auto;
	}

	.fliters-sort i {
		margin-right: 1rem;
	}

	.fliters-sort span {
		font-size: 1.4rem;
	}

	.fliters-sort {
		display: flex;
		align-items: center;
		color: var(--primary-clr);
		font-weight: var(--fw-bold);
		cursor: pointer;
		transition: all 0.2s;
	}

	/* .fliters-sort:hover {
		text-decoration: underline;
	} */
</style>
