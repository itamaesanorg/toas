<script>
	import Menu from '../lib/Menu.svelte';
	import '../app.css';
</script>

<!-- all inside a div -->
<div class="">
	<div class="flex flex-row items-center p-4 bg-orange-200">
		<Menu />
	</div>

	<main class="flex flex-col items-center justify-center p-4 bg-black">
		<slot />
	</main>
</div>
