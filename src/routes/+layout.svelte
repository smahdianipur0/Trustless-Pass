<script lang="ts">

	// Imports:
	import Nav from '$lib/Nav.svelte';
	import '../app.css';
	
</script>


<div class="canv">

<Nav />




<!-- App Content -->
<main><slot />

</main>


</div>


<style>


	main {
		padding: 2px;
		margin-top: var(--portion);
		
			
	}



</style>