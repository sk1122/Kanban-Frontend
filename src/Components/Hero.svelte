<script>
	import Tailwind from './Tailwind.svelte';
	import { user } from './stores';

	let src = "./icons/Kanban.svg"
	console.log($user)
</script>

<Tailwind />

<div class="bg-gradient-to-r from-dark-500 via-dark-400 to-dark-200 container flex md:flex-row sm:flex-col h-full w-full md:items-center sm:justify-center text-white-100">
	<div class="container w-full lg:w-2/3 flex-col flex-wrap">
		<h1 class="mx-8 my-5 text-5xl heading">Manage Your Tasks like a Champ</h1>
		{$user}
		{#if $user === 'true'}
			<div></div>
		{:else}
			<a href="/register" class="mx-8 bg-white-200 px-3 py-2 font-bold  text-dark-400 hover:text-white-100 rounded hover:bg-dark-200 focus:outline-none focus:ring-4 focus:ring-white-200 focus:ring-opacity-50 link">Sign Up Right Now!!</a>
		{/if}
	</div>
	<div class="container sm:hidden md:block w-full lg:w-1/3 pr-5">
		<img {src} alt="Kanban Board">
	</div>
</div>

<style>
	.heading {
		font-family: 'Gilroy';
	}

	.link {
		font-family: 'Inter';
	}
</style>