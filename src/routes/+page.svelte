<script>
	import { v4 as uuid } from 'uuid';
	import TodoList from '../components/TodoList.svelte';
	import Form from '../components/Form.svelte';
	let todos = [
		{
			id: uuid(),
			title: 'First Todo',
			completed: true
		},
		{
			id: uuid(),
			title: 'Second Todo',
			completed: true
		},
		{
			id: uuid(),
			title: 'Third Todo',
			completed: true
		}
	];
	function handleAddTodo(event) {
		todos = [
			...todos,
			{
				id: uuid(),
				title: event.detail.title,
				completed: false
			}
		];
	}
	console.log(todos);
	function handleDeleteTodo(event) {
		todos = todos.filter((todo) => todo.id !== event.detail.id);
	}
</script>

<div class="app-container">
	<TodoList {todos} on:deletetodo={handleDeleteTodo} />
	<Form on:addtodo={handleAddTodo} />
</div>

<style>
	.app-container {
		width: 400px;
		min-height: 500px;
		background-color: #282c34;
		box-shadow: 0 20px 80px rgba(0, 0, 0, 0.6);
		background: radial-gradient(circle, #282c34 0%, rgba(40, 48, 56, 1) 100%);
		position: relative;
		margin: 5% auto;
		border-radius: 1em;
		padding: 20px;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}
</style>
