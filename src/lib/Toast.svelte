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
