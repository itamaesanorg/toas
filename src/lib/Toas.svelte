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
