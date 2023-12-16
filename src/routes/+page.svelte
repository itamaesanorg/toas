<script lang="ts">
	import Toast from '$lib/Toast.svelte';
	import { onMount } from 'svelte';

	onMount(() => {
		(window as any)['showToast']('Hello, World!');
	});
</script>

<Toast />

<div class="flex flex-col space-y-8 p-8 items-center text-white justify-center h-screen">
	<h1 class="text-6xl">🍣JS</h1>
	<div class="text-3xl">
		<h2>
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
