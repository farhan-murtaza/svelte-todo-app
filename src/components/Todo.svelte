<script>
	import { fly } from 'svelte/transition';
	import FaRegTrashAlt from 'svelte-icons/fa/FaRegTrashAlt.svelte';
	import { createEventDispatcher } from 'svelte';

	export let id;
	export let itemTitle;
	export let completed;

	const dispatch = createEventDispatcher();

	function handleToggle(id) {
		console.log('Clicked complete!', id);
		dispatch('toggletodo', {
			id
		});
	}

	function handleDeleteTodo(id) {
		dispatch('deletetodo', {
			id
		});
	}
</script>

<li
	transition:fly={{ y: 200, duration: 2000 }}
	class="todo-list list-item-view {completed ? 'completed' : ''}"
>
	<span>
		<input
			class="btn btn-done"
			type="checkbox"
			checked={completed}
			on:click={() => handleToggle(id)}
		/>
		<span class="title">{itemTitle}</span>
	</span>

	<span class="btn icon" on:click={() => handleDeleteTodo(id)}>
		<FaRegTrashAlt />
	</span>
</li>

<style>
	.btn {
		color: inherit;
		cursor: pointer;
		font-size: 15px;
		padding: 10px 12px;
		border-radius: 2em;
		background: none;
		border: 0px solid;
		transition: 250ms ease-out;
	}

	.btn:hover {
		background: #1d2025;
	}

	.btn:focus {
		outline: none;
	}
	.icon {
		width: 12px;
		color: yellow;
	}
	.list-item-view {
		padding-top: 5px;
		padding-bottom: 0px;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.completed {
		color: #6a6f75;
		opacity: 0.5;
	}
	.title {
		color: #fff;
	}
</style>
