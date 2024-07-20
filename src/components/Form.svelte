<script>
	import FaPlus from 'svelte-icons/fa/FaPlus.svelte';
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

	export let inputText = '';
	let input;
	export function clearInput() {
		inputText = '';
	}
	export function focusInput() {
		input.focus();
	}
	function handleAddTodo() {
		if (!inputText) return;
		dispatch('addtodo', {
			title: inputText
		});
	}
</script>

<!-- Add form at bottom -->
<form class="app-form" on:submit|preventDefault={handleAddTodo}>
	<input
		bind:this={input}
		placeholder="Add Todo.."
		type="text"
		class="input-text"
		name=""
		bind:value={inputText}
	/>
	<button type="submit" class="btn"><FaPlus /></button>
</form>

<style>
	.app-form {
		margin-bottom: 10px;
		display: flex;
		justify-content: center;
	}

	.input-text {
		height: 40px;
		background: #282c34;
		font-size: 15px;
		border: 1px solid #a2a8ad;
		color: #dce4ec;
		width: 100%;
		margin-right: 15px;
		border-radius: 2em;
		padding: 5px 10px;
		transition: border 250ms ease-out;
	}

	.input-text:focus {
		border: 1px solid #ffffff;
		background: #1d2025;
		outline: none;
		color: #dce4ec;
	}

	::placeholder {
		opacity: 0.3;
	}

	.btn {
		width: 40px;
		color: #fff;
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
</style>
