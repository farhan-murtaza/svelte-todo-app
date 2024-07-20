<script>
	import { v4 as uuid } from 'uuid';
	import TodoList from '../components/TodoList.svelte';
	import Form from '../components/Form.svelte';
	import { onDestroy } from 'svelte';
	let formInput;
	onDestroy(() => {
		console.log('Destroyed');
	});

	let showList = true;
	let todos = [
		{
			id: uuid(),
			title: 'First Todo',
			completed: true
		},
		{
			id: uuid(),
			title: 'Second Todo',
			completed: false
		},
		{
			id: uuid(),
			title: 'Third Todo',
			completed: true
		}
	];
	function handleAddTodo(event) {
		event.preventDefault();
		setTimeout(() => {
			todos = [
				...todos,
				{
					id: uuid(),
					title: event.detail.title,
					completed: false
				}
			];
			formInput.clearInput();
			formInput.focusInput();
		}, 300);
	}
	function handleDeleteTodo(event) {
		todos = todos.filter((todo) => todo.id !== event.detail.id);
	}
	function handleToggleTodo(event) {
		todos = todos.map((todo) => {
			if (todo.id === event.detail.id) {
				return { ...todo, completed: event.detail.value };
			}
			return { ...todo };
		});
	}
</script>

<div class="app-container">
	<label>
		Hide your Todos
		<input type="checkbox" bind:checked={showList} />
	</label>
	{#if showList}
		<TodoList {todos} on:deletetodo={handleDeleteTodo} on:toggletodo={handleToggleTodo} />
	{/if}
	<Form bind:this={formInput} on:addtodo={handleAddTodo} />
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
	label {
		height: 30%;
		width: 70%;
		font-size: 1.6rem;
		font-weight: bold;
		color: #fff;
	}
	label > input {
		width: 25px;
		height: 15px;
	}
</style>
