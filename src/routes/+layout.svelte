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
		padding: 1rem;
		margin-top: var(--small-portion);
		
			
	}

	.canv{
	min-height: max-content;
  	min-height: 100vh;
	background-image: url($lib/dddepth-198.webp);
/*background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' version='1.1' xmlns:xlink='http://www.w3.org/1999/xlink' xmlns:svgjs='http://svgjs.dev/svgjs' width='1120' height='1120' preserveAspectRatio='none' viewBox='0 0 1120 1120'%3e%3cg clip-path='url(%26quot%3b%23SvgjsClipPath1327%26quot%3b)' fill='none'%3e%3crect width='1120' height='1120' x='0' y='0' fill='rgba(20%2c 20%2c 20%2c 1)'%3e%3c/rect%3e%3ccircle r='68.69' cx='876.25' cy='884.49' fill='url(%26quot%3b%23SvgjsLinearGradient1328%26quot%3b)'%3e%3c/circle%3e%3ccircle r='48.085' cx='346.49' cy='788.15' fill='url(%26quot%3b%23SvgjsLinearGradient1329%26quot%3b)'%3e%3c/circle%3e%3ccircle r='46.58' cx='271.38' cy='956.05' fill='url(%26quot%3b%23SvgjsLinearGradient1330%26quot%3b)'%3e%3c/circle%3e%3ccircle r='44.93' cx='798.41' cy='500.07' fill='url(%26quot%3b%23SvgjsLinearGradient1331%26quot%3b)'%3e%3c/circle%3e%3ccircle r='63.11' cx='315.33' cy='496.79' fill='url(%26quot%3b%23SvgjsLinearGradient1332%26quot%3b)'%3e%3c/circle%3e%3ccircle r='65.855' cx='428.97' cy='745.13' fill='url(%26quot%3b%23SvgjsLinearGradient1333%26quot%3b)'%3e%3c/circle%3e%3ccircle r='34.44' cx='837.6' cy='516.02' fill='url(%26quot%3b%23SvgjsLinearGradient1334%26quot%3b)'%3e%3c/circle%3e%3c/g%3e%3cdefs%3e%3cclipPath id='SvgjsClipPath1327'%3e%3crect width='1120' height='1120' x='0' y='0'%3e%3c/rect%3e%3c/clipPath%3e%3clinearGradient x1='738.87' y1='884.49' x2='1013.63' y2='884.49' gradientUnits='userSpaceOnUse' id='SvgjsLinearGradient1328'%3e%3cstop stop-color='%2384b6e0' offset='0.1'%3e%3c/stop%3e%3cstop stop-color='%23464a8f' offset='0.9'%3e%3c/stop%3e%3c/linearGradient%3e%3clinearGradient x1='250.32' y1='788.15' x2='442.65999999999997' y2='788.15' gradientUnits='userSpaceOnUse' id='SvgjsLinearGradient1329'%3e%3cstop stop-color='%23ab3c51' offset='0.1'%3e%3c/stop%3e%3cstop stop-color='%234f4484' offset='0.9'%3e%3c/stop%3e%3c/linearGradient%3e%3clinearGradient x1='178.22' y1='956.05' x2='364.53999999999996' y2='956.05' gradientUnits='userSpaceOnUse' id='SvgjsLinearGradient1330'%3e%3cstop stop-color='%2332325d' offset='0.1'%3e%3c/stop%3e%3cstop stop-color='%23424488' offset='0.9'%3e%3c/stop%3e%3c/linearGradient%3e%3clinearGradient x1='708.55' y1='500.07' x2='888.27' y2='500.07' gradientUnits='userSpaceOnUse' id='SvgjsLinearGradient1331'%3e%3cstop stop-color='%2384b6e0' offset='0.1'%3e%3c/stop%3e%3cstop stop-color='%23464a8f' offset='0.9'%3e%3c/stop%3e%3c/linearGradient%3e%3clinearGradient x1='189.10999999999999' y1='496.7900000000001' x2='441.54999999999995' y2='496.7900000000001' gradientUnits='userSpaceOnUse' id='SvgjsLinearGradient1332'%3e%3cstop stop-color='%23f29b7c' offset='0.1'%3e%3c/stop%3e%3cstop stop-color='%237e6286' offset='0.9'%3e%3c/stop%3e%3c/linearGradient%3e%3clinearGradient x1='297.26' y1='745.13' x2='560.6800000000001' y2='745.13' gradientUnits='userSpaceOnUse' id='SvgjsLinearGradient1333'%3e%3cstop stop-color='%23ab3c51' offset='0.1'%3e%3c/stop%3e%3cstop stop-color='%234f4484' offset='0.9'%3e%3c/stop%3e%3c/linearGradient%3e%3clinearGradient x1='768.72' y1='516.02' x2='906.48' y2='516.02' gradientUnits='userSpaceOnUse' id='SvgjsLinearGradient1334'%3e%3cstop stop-color='rgba(226%2c 152%2c 222%2c 1)' offset='0.1'%3e%3c/stop%3e%3cstop stop-color='rgba(72%2c 70%2c 135%2c 1)' offset='0.9'%3e%3c/stop%3e%3c/linearGradient%3e%3c/defs%3e%3c/svg%3e");*/
	background-repeat: no-repeat;
    background-size: cover;
    background-position: 0 0;
    border: 0.1px solid transparent ;

	}

</style>