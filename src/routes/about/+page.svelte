<script lang="ts">

  //Title
  import { title } from '$lib/titleStore';
  title.set('About');

	// Imports:
	import { onMount } from 'svelte';

	// Initializations & Exports:
	// :3

	onMount(() => {
		// :3
	});
	
</script>


<svelte:head>
	<title>About</title>
	<meta name="description" content="About Page" />
</svelte:head>

<!-- Page Content -->
<section>
	<span>
		<br>
		
		
		<span style="display: grid; justify-content: center ; " >

			Template : <a class="anchor" href="https://github.com/Ncookiez">Ncookiez</a>
		<br>
		Encrypt / Decryptg template :  <a class="anchor" href=" https://asecuritysite.com/">asecuritysite</a>
		<br>
		realistic password strength estimation : <a class="anchor" href="https://dropbox.tech/security/zxcvbn-realistic-password-strength-estimation">zxcvbn</a>
		<br>
		Framework : <a class="anchor" href="https://kit.svelte.dev/">Sveltekit</a>
		<br>
		
		Rust and WebAssembly tutorial : <a class="anchor" href="https://www.youtube.com/channel/UC2S3Qt_thQx0vk6zDaE8Lqw">SvelteRust</a>
		<br>
		icon : <a class="anchor" href="https://iconscout.com/contributors/ncrte3d">Naufal Imaanullah</a>
		<br>
		
				
		</span>
</section>



<style>

a{
color: var(--accent-border);
}

	
</style>