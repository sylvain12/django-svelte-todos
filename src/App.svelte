<script>
	import { onMount } from 'svelte';
	import AddTodo from './components/AddTodo.svelte';
	import Header from './components/Header.svelte';
	import Todos from './components/Todos.svelte';
	let todos = [];
	const BASE_URL = 'http://127.0.0.1:8081/api';
	const TODOS_API_URL = 'http://127.0.0.1:8081/api/todos/';

	onMount(async () => {
		const response = await fetch(TODOS_API_URL);
		todos = await response.json();
		console.log(todos);
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

		console.log(result);
	};
</script>

<main>
	<Header />
	<AddTodo on:addTodo={(event) => handleAdd(event.detail)} />

	<Todos {todos} on:deleteTodo={(event) => handleDelete(event)} on:toggleComplete={(event) => handleToggleCompleted(event)} />
</main>

<style>
	main {
		max-width: 765px;
		width: 90%;
		margin: 0 auto;
	}
</style>
