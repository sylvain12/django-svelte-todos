<script>
	export let todosCount = 23;
</script>

<div class="header">
	<h1>Tasks</h1>

	<span>{todosCount}</span>
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

	.header span {
		display: inline-block;
		width: 3rem;
		height: 3rem;
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
		color: #fff;
		background-color: var(--primary-clr);
		font-size: 1.2rem;
		line-height: 0;
	}
</style>
