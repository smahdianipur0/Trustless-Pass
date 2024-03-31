<script lang="ts">

	// Imports:
	import Nav from '$lib/Nav.svelte';
	import '../app.css';
	
</script>


<div>

<Nav />




<!-- App Content -->
<main><slot />

</main>


</div>


<style>


	main {
		padding: 1rem;
		margin-top: var(--small-portion);
		
			
	}

	div{
	min-height: max-content;
  	min-height: 100vh;
	background-image: url($lib/dddepth-153.png);
	background-repeat: no-repeat;
    background-size: cover;

	}

</style>