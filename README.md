> [!NOTE]  
> This is in pre-beta

# Initial config
Toas is a web component that will allow you to add notifications without the need of an external library.

## Component

```svelte
<script>
	import { onMount } from 'svelte';
	let show = false;
	let message = '';

	// @ts-ignore
	function showToas(msg) {
		if (!msg) {
			console.error('No message provided for toas');
			return;
		}
		message = msg;
		show = true;
		setTimeout(() => {
			show = false;
		}, 3000);
	}

	onMount(() => {
		if (!window) {
			console.error('Window object is not available');
			return;
		}
		// @ts-ignore
		window['showToas'] = showToas;
	});
</script>

{#if show}
	<div class="toas">
		{message}
	</div>
{/if}

<style>
	.toas {
		position: fixed;
		top: 2%;
		left: 50%;
		transform: translateX(-50%);
		background-color: #333;
		color: #fff;
		padding: 10px;
		border-radius: 5px;
		z-index: 9999;
	}
</style>
```

## Use case

```svelte
<script>
	import Toas from '$lib/Toas.svelte';
	import { onMount } from 'svelte';

	onMount(() => {
		// @ts-ignore
		window['showToas']('Hello, World!');
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
</div>
```