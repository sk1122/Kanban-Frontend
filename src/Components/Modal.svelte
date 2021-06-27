<script>
	import { visibleTodoModal, columnData } from './stores'
	import { addTodo, updateTodo, getTodo } from '../Lib/Board'
	import { useEffect } from '../Lib/hooks'

	let main
	let todo_name
	let todo_desc

	$: if($visibleTodoModal[0] == "true") {
		main.classList.remove('hidden')
	}
	console.log('dsa')
	const closeModal = () => {
		main.classList.add("hidden")
		visibleTodoModal.update(visibleTodoModal => ['false', '0', 'false'])
	}

	const submitForm = () => {
		console.log('dsa')
		if($visibleTodoModal[2] == 'true') {
			console.log('Huh')
			addTodo(todo_name, todo_desc, $visibleTodoModal[1]).then(res => $columnData = [...$columnData, JSON.parse(res).todo])
		} else {
			var todo = JSON.stringify({
				todo_id: $visibleTodoModal[1].id,
				todo_name: $visibleTodoModal[1].todo_name,
				todo_desc: $visibleTodoModal[1].todo_desc
			})
			updateTodo(todo)
			getTodo().then(res => {$columnData = res; console.log($columnData)})
		}
		closeModal()
	}
</script>

<main bind:this={main} class="hidden absolute filter drop-shadow-lg rounded blur-0 bottom-40 left-1/3 -translate-x-2/4 -translate-y-2/4 w-96 h-3/4 bg-dark-400" style="font-family: 'Inter'">
	<div on:click={closeModal} class="absolute right-5 top-5 cursor-pointer">
		<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white-200 hover:text-white-100" viewBox="0 0 20 20" fill="currentColor">
			<path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd" />
		</svg>
	</div>
	<div class="w-full h-full flex flex-col items-center">
		<div class="flex justify-center items-center container w-full h-1/4">
			{#if $visibleTodoModal[2] == 'true'}
				<h1 class="text-3xl text-center text-white-100 font-extrabold" >Add Todo</h1>
			{:else}
				<h1 class="text-3xl text-center text-white-100 font-extrabold">Todo Details</h1>
			{/if}
		</div>

		<div class="flex flex-col items-center w-full h-3/4">
			<div class="col mt-8 sm:ml-2 sm:mt-0 sm:w-2/3">
				<div class="box border rounded flex flex-col shadow bg-white">
					<div class="box__title bg-white-200 px-3 py-2 border-b">
						<h3 class="text-sm text-grey-darker font-medium">What do you want to do?</h3>
					</div>
					{#if $visibleTodoModal[2] == 'true'}
						<input bind:value={todo_name} type="text" class="appearance-none rounded-none relative block w-full px-3 py-2 placeholder-dark-100 text-dark-500 focus:z-10 sm:text-2xl">
					{:else}
						<input bind:value={$visibleTodoModal[1].todo_name} type="text" class="appearance-none rounded-none relative block w-full px-3 py-2 placeholder-dark-100 text-dark-500 focus:z-10 sm:text-2xl">
					{/if}
				</div>
			</div>

			<div class="col mt-8 sm:ml-2 mb-8 sm:mt-8 sm:w-2/3">
				<div class="box border rounded flex flex-col shadow bg-white">
					<div class="box__title bg-white-200 px-3 py-2 border-b">
						<h3 class="text-sm text-grey-darker font-medium">Todo Description</h3>
					</div>
					{#if $visibleTodoModal[2] == 'true'}
						<textarea bind:value={todo_desc} maxlength="120" class="text-grey-darkest flex-1 bg-transparent" name="tt"></textarea>
					{:else}
						<textarea bind:value={$visibleTodoModal[1].todo_desc} maxlength="120" class="text-grey-darkest flex-1 bg-transparent" name="tt"></textarea>
					{/if}
				</div>
			</div>

			<div class="w-full flex justify-center items-center">
				<div class="btn">
					<button on:click={submitForm} class="transition duration-500 ease-in-out rounded bg-white-200 text-dark-500 hover:bg-white-100 hover:text-dark-400 transform hover:-translate-y-1 hover:scale-110 py-2 px-2" >	
						{#if $visibleTodoModal[2] == 'true'}
							Create Todo
						{:else}
							Update Todo
						{/if}
					</button>
				</div>
			</div>
		</div>
	</div>
</main>