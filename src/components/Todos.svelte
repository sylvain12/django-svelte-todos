<script>
	export let todos = [];
</script>

{#each todos as todo (todo.id)}
	<div class={todo.completed ? 'todo-item todo-item-completed' : 'todo-item'}>
		<span class="todo-item-content">{todo.title}</span>
		<div class="todo-item-action">
			<button class="btn">Edit</button>
			<button class="btn">Delelte</button>
		</div>
	</div>
{:else}
	<p>No todos found</p>
{/each}

<style>
	.todo-item {
		font-size: 1.4rem;
		padding: 1.5rem 0;
		border-left: 3px solid;
		padding-left: 1rem;
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
</style>
