> [!NOTE]  
> This is in pre-beta

![Toas Header Image](./static/toast.jpg)

Thanks for your support Vite
![Thanks for your support Vite](./static/support.png)
Source: [https://x.com/MiguelGargallo/status/1736023947810885761?s=20](https://x.com/MiguelGargallo/status/1736023947810885761?s=20)

- [Usage](#usage)
- [Initial config](#initial-config)
	- [In this version](#in-this-version)
	- [How to use it](#how-to-use-it)
- [About the License](#about-the-license)

## Usage

Look, you add the export function you can look at the directory for a [Real case](./realcase/Component.svelte.md)

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

## Initial config
Toas is a web component that will allow you to add notifications without the need of an external library.

### In this version
We added colors to the notifications, and we are currently working on icons.

### How to use it
Just copy and paste the code from [here](./src/lib/Toas.svelte) and use it like this file [here](./src/routes/+page.svelte).

## About the License
This project is under the [Pylar AI Creative ML Free License](./License.md).