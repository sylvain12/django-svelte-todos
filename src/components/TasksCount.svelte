<script>
	export let counter = {};
</script>

<div class="tasks-count-list">
	<span class="task-count-item task-count-item-primary">{counter.allTodosCount}</span>
	<span class="task-count-item task-count-item-success">{counter.activeTodosCount}</span>
	<span class="task-count-item task-count-item-danger">{counter.completedTodosCount}</span>
</div>

<style>
	.tasks-count-list {
		display: flex;
		align-items: center;
	}

	span {
		display: inline-block;
		width: 3rem;
		height: 3rem;
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
		color: #fff;
		font-size: 1.2rem;
		line-height: 0;
	}

	span:not(:last-child) {
		margin-right: 1rem;
	}

	.task-count-item-primary {
		background-color: var(--primary-clr);
	}

	.task-count-item-success {
		background-color: var(--success-clr);
	}

	.task-count-item-danger {
		background-color: var(--danger-clr);
	}
</style>
