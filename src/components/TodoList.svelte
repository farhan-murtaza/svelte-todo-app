<script>
	import Todo from './Todo.svelte';

	export let todos;
</script>

<!-- List of actual todos -->
<div class="app-body">
	{#if todos.length === 0}
		<p class="app-body__empty">No todos Yet</p>
	{:else}
		<ul>
			{#each todos as todo}
				<Todo
					id={todo.id}
					itemTitle={todo.title}
					completed={todo.completed}
					on:deletetodo
					on:toggletodo
				/>
			{/each}
		</ul>
	{/if}
</div>

<style>
	ul {
		border-top: 1px solid rgb(121, 121, 121);
		padding-top: 10px;
		list-style-type: none;
		padding-left: 0px;
	}

	.app-body {
		flex-grow: 1;
		max-height: 400px;
		/* overflow-x: hidden; */
		scrollbar-gutter: none;
		-ms-overflow-style: none; /* IE and Edge */
		scrollbar-width: none; /* Firefox */
		overflow: hidden;
		overflow-y: scroll;
	}
	.app-body__empty {
		text-align: center;
		margin: 45% auto;
		width: 50%;
		font-size: 1.7rem;
		color: #fff;
	}
</style>
