<script lang="ts">

	import { title } from '$lib/titleStore';
  title.set('QR Code Generator');




  import { QRCodeImage } from "svelte-qrcode-image";

  
	let text = '';


	
</script>





<div class= "page">
<div >
	<title>Generate QR Code</title>
<p class="title">Generate QR Code</p>
<div class="card-1 dark glass small-shadow" >  



<textarea  class="txt-area dark glass " rows="2"
							 bind:value={text} placeholder="Please enter some text."></textarea>



	{#if text}


<div class="qr">
					<QRCodeImage text={text} width={160} height={160} margin={1} />
					
</div>
{/if}
</div>	
</div>
</div>


   








<style>


	
	
</style>