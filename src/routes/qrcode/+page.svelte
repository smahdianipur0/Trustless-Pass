<script lang="ts">

	import { title } from '$lib/titleStore';
  title.set('QR Code Generator');
  	import { copy }  from 'svelte-copy';


  //Toast:
	 import { onMount } from 'svelte';
	 let isToastOpen = false;
   let timeoutId:number;

  function toggleToast() {
    isToastOpen = !isToastOpen;  
    if (isToastOpen) {
      timeoutId = setTimeout(() => {
        isToastOpen = false;
      }, 2000);
    } else {
      clearTimeout(timeoutId);
    }
  }

  onMount(() => {
    return () => {
      clearTimeout(timeoutId);
    };
  });



  import { QRCodeImage } from "svelte-qrcode-image";

  
	let text = '';

	function isValid(text: string) {
    return (
      text !== ""
    );
	}

  let showQR = false;
  function toggleQR() {
    showQR = !showQR }
	
</script>



<body  id ="display-toast">
<div class="card">
<div class= "page">


													  		

<div class="card-2">
	<title>Generate QR Code</title>
<p style = "font-weight: bold; font-size: 18px; margin-bottom: 10px;">&nbsp &nbsp Generate QR Code</p>
<div class="card-1 dark glass small-shadow" >  



<textarea  class="txt-area dark glass" rows="2"
							 bind:value={text} placeholder="Please enter some text."></textarea>



	{#if text}

<div class="btn-group  "> 

				
	      	<button  use:copy={text}  class="main" > <a href="/qrcode#" on:click={toggleToast}> Copy </button>
					<button class="main" on:click={toggleQR}> Show QR Code</button>
				</div>
				{:else}
				<div class="btn-group  "> 
					<button class="main disabled "> Copy</button>
					<button class="main disabled "> Show QR Code</button>
				</div>

				{/if}
			<div class="qr">
			{#if showQR && text }

					<QRCodeImage class="qr" text={text} width={160} height={160} margin={1} />
					{/if}
</div>	
</div>
</div>
</div>
</div>
    <div class="toast dark glass" class:opentoast={isToastOpen}> Copied 

</div>
</body>







<style>


	
	
</style>