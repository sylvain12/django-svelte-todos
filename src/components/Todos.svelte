<script>
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();
	export let todos = [];
</script>

{#each todos as todo (todo.id)}
	<div class={todo.completed ? 'todo-item todo-item-completed' : 'todo-item'}>
		<span class="todo-item-content">{todo.title}</span>
		<div class="todo-item-action">
			<!-- <button class="btn btn-outline-success">
				<i class="fi-rr-pencil" />
			</button> -->
			<button class="btn btn-outline-danger" on:click={() => dispatch('deleteTodo', todo.id)}>
				<i class="fi-rr-cross" />
			</button>
		</div>
	</div>
{:else}
	<p>No todos found</p>
{/each}

<style>
	.todo-item {
		font-size: 1.4rem;
		padding: 1.5rem 1rem;
		border-left: 3px solid;
		background-color: #fff;
		border-left-color: var(--success-clr);
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.todo-item:not(:last-child) {
		/* border-bottom: 1px solid rgb(228, 228, 228); */
		margin-bottom: 2rem;
	}

	.todo-item.todo-item-completed {
		border-color: var(--danger-clr);
		font-weight: var(--fw-light);
		opacity: 0.45;
	}

	.todo-item.todo-item-completed .todo-item-content {
		text-decoration: line-through;
	}

	.todo-item-action {
		display: flex;
		justify-content: flex-end;
		align-items: center;
	}

	.todo-item-action button:not(:last-child) {
		margin-right: 0.5rem;
	}

	.todo-item-action button i {
		font-size: 1.3rem;
	}

	.btn {
		display: inline-block;
		text-decoration: none;
		/* padding: 0.8rem; */
		cursor: pointer;
		border: none;
		background-color: transparent;
		border-radius: 50%;
	}

	.btn:hover {
	}

	.btn-outline-danger {
		color: var(--danger-clr);
	}

	.btn-outline-success {
		color: var(--success-clr);
	}
</style>
