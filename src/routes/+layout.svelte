<script lang="ts">

	// Imports:
	import Nav from '$lib/Nav.svelte';
	import '../app.css';
	
</script>




<Nav />




<!-- App Content -->
<main><slot />
<br>
<br>
<br>
</main>





<style>


	main {
		padding: 1rem;
		margin-top: var(--small-portion);

	}

</style>