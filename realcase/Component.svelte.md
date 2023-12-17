```svelte
<!-- Component.svelte -->

<script>
	import PocketBase from 'pocketbase';
	import Toas from '$lib/Toas.svelte';

	function handleSuccessClick() {
		// @ts-ignore
		window['showToas']('Operation Successful', 'success');
	}
	function handleLoadingClick() {
		// @ts-ignore
		window['showToas']('Operation in progress', 'loading');
	}

	const pb = new PocketBase(import.meta.env.VITE_DATABASE);

	/**
	 * @type {any[]}
	 */
	let records = [];

	const fetchRecords = async () => {
		try {
			const recordsData = await pb.collection('users').getFullList();
			records = recordsData;
			handleSuccessClick();
		} catch (err) {
			console.log(err);
		}
	};

	fetchRecords();

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