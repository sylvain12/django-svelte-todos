<script>
	import { onMount } from 'svelte';
	import AddTodo from './components/AddTodo.svelte';
	import Header from './components/Header.svelte';
	import Todos from './components/Todos.svelte';
	let todos = [];
	const TODOS_API_URL = 'http://127.0.0.1:8081/api/todos/';

	onMount(async () => {
		const response = await fetch(TODOS_API_URL);
		todos = await response.json();
		console.log(todos);
	});

	const add = async (todoTitle) => {
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
</script>

<main>
	<Header />
	<AddTodo on:addTodo={(event) => add(event.detail)} />
	<Todos {todos} />
</main>

<style>
	main {
		max-width: 765px;
		width: 90%;
		margin: 0 auto;
	}
</style>
