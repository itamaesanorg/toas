<script>
	import Toas from '$lib/Toas.svelte';
	import { onMount } from 'svelte';

	function handleSuccessClick() {
		// @ts-ignore
		window['showToas']('Operation Successful', 'success');
	}

	function handleLoadingClick() {
		// @ts-ignore
		window['showToas']('Operation Loading', 'loading');
	}

	function handleErrorClick() {
		// @ts-ignore
		window['showToas']('Operation Failed', 'error');
	}

	onMount(() => {
		// @ts-ignore
		window['showToas']('Hello, World!', 'onmount');
	});
</script>

<Toas />

<div class="flex flex-col space-y-8 p-8 items-center text-white justify-center h-screen bg-black">
	<h1 class="text-6xl">🍞 Toas</h1>
	<div class="text-3xl">
		<h2>
			Toas is a
			<span class="text-orange-400 font-bold">SvelteKit 2</span>
			with
			<span class="text-pink-400 font-bold">Vite 5</span>
			web component.
		</h2>
		<br />
		<h2>
			Just
			<span class="text-green-400 font-bold">import</span>
			to use.
		</h2>
		<br />
		<h2>
			<span class="text-blue-400 font-bold">No</span>
			dependencies.
		</h2>
	</div>
	<div class="flex flex-row space-x-8 text-black font-bold">
		<button
			on:click={handleSuccessClick}
			class="mt-4 px-4 py-2 bg-green-500 rounded shadow-md hover:shadow-lg shadow-green-500 hover:shadow-green-800"
		>
			Success
		</button>
		<button
			on:click={handleLoadingClick}
			class="mt-4 px-4 py-2 bg-yellow-500 rounded shadow-md hover:shadow-lg shadow-yellow-500 hover:shadow-yellow-800"
		>
			Loading
		</button>
		<button
			on:click={handleErrorClick}
			class="mt-4 px-4 py-2 bg-red-500 rounded shadow-md hover:shadow-lg shadow-red-500 hover:shadow-red-800"
		>
			Error
		</button>
	</div>
</div>

<style>
	button {
		transition: transform 0.3s ease;
	}

	button:hover {
		transform: scale(1.1);
	}

	button:active {
		transform: scale(0.9);
	}
</style>
