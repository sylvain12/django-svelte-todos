<script>
	import { onMount, beforeUpdate } from 'svelte';
	import AddTodo from './components/AddTodo.svelte';
	import ClearCompleted from './components/ClearCompleted.svelte';
	import Filters from './components/Filters.svelte';
	import Header from './components/Header.svelte';
	import Todos from './components/Todos.svelte';

	const BASE_URL = 'http://127.0.0.1:8081/api';
	const TODOS_API_URL = 'http://127.0.0.1:8081/api/todos/';
	let title;
	let defaultView;
	let sortDirection;

	$: filterTodos = [];

	let todos = [];

	$: handleViewChange = () => {
		switch (defaultView) {
			case 'active':
				filterTodos = todos.filter((todo) => !todo.completed);
				break;

			case 'completed':
				filterTodos = todos.filter((todo) => todo.completed);
				break;

			default:
				filterTodos = todos;
				break;
		}
	};

	onMount(async () => {
		const response = await fetch(TODOS_API_URL);
		todos = await response.json();
		handleViewChange();
	});

	beforeUpdate(() => {
		handleViewChange();
	});

	const handleAdd = async (todoTitle) => {
		const response = await fetch(TODOS_API_URL, {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json',
				Accept: 'application/json',
			},
			body: JSON.stringify({ title: todoTitle }),
		});

		const newTodo = await response.json();
		todos = [newTodo, ...todos];
		title = '';
	};

	const handleDelete = async (event) => {
		const response = await fetch(`${BASE_URL}/todo/${event.detail}/`, {
			method: 'DELETE',
			headers: {
				'Content-Type': 'application/json',
				Accept: 'application/json',
			},
		});
		const result = await response.status;

		todos = todos.filter((todo) => todo.id !== event.detail);
	};

	const handleToggleCompleted = async (event) => {
		const response = await fetch(`${BASE_URL}/todo/${event.detail.id}/`, {
			method: 'PATCH',
			headers: {
				'Content-Type': 'application/json',
				Accept: 'application/json',
			},
			body: JSON.stringify({ completed: !event.detail.completed }),
		});

		const result = await response.json();
	};

	// const handleClearCompleted = async () => {
	// 	todos.map((todo) => {
	// 		if (!todo.completed) {
	// 			handleDelete(todo.id);
	// 		}
	// 	});
	// };

	const handleSort = () => {
		if (sortDirection === 1) {
			filterTodos = filterTodos.sort((t1, t2) => (t1.title.toLowerCase() < t2.title.toLowerCase() ? 1 : -1));
			// filterTodos = filterTodos.sort((t1, t2) => t1.name - t2.name);
			sortDirection = 2;
		} else if (sortDirection === 2) {
			filterTodos = filterTodos.sort((t1, t2) => (t1.title.toLowerCase() > t2.title.toLowerCase() ? 1 : -1));
			sortDirection = 1;
		}
	};
</script>

<main>
	<Header />

	<AddTodo {title} on:addTodo={(event) => handleAdd(event.detail)} />

	<div class="flex">
		<Filters bind:sortDirection bind:view={defaultView} on:sortTodos={handleSort} />
		<!-- <ClearCompleted on:click={handleClearCompleted} /> -->
	</div>

	<Todos bind:todos={filterTodos} on:deleteTodo={(event) => handleDelete(event)} on:toggleComplete={(event) => handleToggleCompleted(event)} />
</main>

<style>
	main {
		max-width: 765px;
		width: 90%;
		margin: 0 auto;
	}

	.flex {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 2rem;
	}
</style>
