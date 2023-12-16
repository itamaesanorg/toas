> [!NOTE]  
> This is in pre-beta

# Initial config
It is a skeleton project, using JavaScript with JSDoc comments, also we added ESLint for code linting, Prettier for code formatting and Vitest for unit testing

## First Optimization
We added our own toast system:

### Sushi Toast

```svelte
<script lang="ts">
	import { onMount } from 'svelte';
	let show = false;
	let message = '';

	function showToast(msg: string) {
		if (!msg) {
			console.error('No message provided for toast');
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
		(window as any)['showToast'] = showToast;
	});
</script>

{#if show}
	<div class="toast">
		{message}
	</div>
{/if}

<style>
	.toast {
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

It works directly on the components and pages, no need to go html

```svelte
<script lang="ts">
	import Toast from '$lib/Toast.svelte';
	import { onMount } from 'svelte';
	import { IconHeart } from '@tabler/icons-svelte';

	onMount(() => {
		(window as any)['showToast']('Hello, World!');
	});
</script>

<Toast />

<div class="flex flex-col space-y-8 p-8 items-center text-white justify-center h-screen">
	<h1 class="text-6xl">🍣JS</h1>
	<div class="text-3xl">
		<h2>
			<IconHeart class="inline-block w-8 h-8 text-white" />
			Hello from
			<span class="text-orange-400 font-bold">SvelteKit 2</span>
			with
			<span class="text-pink-400 font-bold">Vite 5</span>
		</h2>
	</div>
	<div class="text-2xl">
		<h2 class="flex flex-col items-center p-2">
			SushiJS also comes with
			<span class="text-green-400 font-bold p-2">PocketBase</span>
			and
			<span class="text-blue-400 font-bold p-2">WC-Toast</span>
		</h2>
	</div>
</div>

<style lang="postcss">
	:global(html) {
		background-color: theme(colors.black);
	}
</style>
```