```svelte
<!-- Component.svelte -->

<script>
	import { onMount } from 'svelte';
	import PocketBase from 'pocketbase';
	import Toas from '$lib/Toas.svelte';

	let records = [];
	const pb = new PocketBase(import.meta.env.VITE_DATABASE);

	function showToas(message, type) {
		if (typeof window !== 'undefined') {
			// @ts-ignore
			window['showToas'](message, type);
		}
	}

	onMount(async () => {
		showToas('Operation in progress', 'loading');
		try {
			const recordsData = await pb.collection('users').getFullList();
			records = recordsData;
			showToas('Operation Successful', 'success');
		} catch (err) {
			showToas('Operation Failed', 'error');
			console.log(err);
		}
	});

	export { records };
</script>

<Toas />

<div class="flex flex-col space-y-4 p-4">
	<h1 class="text-4xl font-bold">Users</h1>
	{#each records as record}
		<div class="flex flex-row space-x-4 text-black">
			<br />
			<p>
				<strong>id:</strong>
				{record.id}
			</p>
			<p>
				<strong>email:</strong>
				{record.email}
			</p>
		</div>
	{/each}
</div>
```