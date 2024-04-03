<script lang="ts" >

	//House keeping
  import { title } from '$lib/titleStore'; title.set('Home');
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



  //Generate Password
  import { generate_password } from "$lib/pkg/rust_lib";

  let password_length = 16

  let add_special_char = true
  function f_add_special_char() {
    add_special_char = !add_special_char; }
    
  let add_number = true
  function f_add_number() {
    add_number = !add_number; }


  let capitalize_first_letter = true
  function f_capitalize_first_letter() {
    capitalize_first_letter = !capitalize_first_letter; }


  let manualEntry = false; 

    function setManualEntryToFalse() {
    manualEntry = true;	
    manualEntry = false;
  }

  let password = '';

  $: if (manualEntry) {
  password = ''; 
  } else {
    password = generate_password(password_length, add_special_char, add_number, capitalize_first_letter);
  }


//calculate password strength
  import { calculate_password_strength }  from "$lib/pkg/rust_lib";
	import { calculate_password_strength2 } from "$lib/pkg/rust_lib";
	import { guessable }                    from "$lib/pkg/rust_lib";

  $: guess = guessable(password);
  $: strength = calculate_password_strength(password);
  $: strength2 = calculate_password_strength2(password);

	$: boxClass = `box ${guess .replace(/\s+/g, '-')}`;



// Count Characters
  import { count_characters }  from "$lib/pkg/rust_lib";

	let Key = '';
  $: Key_count = count_characters(Key);

  let IV = '';
  $: IV_count = count_characters(IV);


//encrypt and decrypt
  import { encrypt } from "$lib/pkg/rust_lib";
  import { decrypt } from "$lib/pkg/rust_lib";

  let plain_text = '';
  let auto_plain = false;
  function f_auto_plain() {
    auto_plain = !auto_plain; } 


  $: if (auto_plain) {
  plain_text = password; 
  } else {
    plain_text = '';
  }

 	let result_e = '';
 	let cipher_text = '';
  let result_d = '';

 
  $: result_e = encrypt(Key,IV,plain_text);
  $: result_d = decrypt(Key,IV,cipher_text);



	//Qr code
  import { QRCodeImage } from "svelte-qrcode-image";

  let showQR_e = false;
  function toggleQR_e() {
    showQR_e = !showQR_e }

 let showQR_d = false;
  function toggleQR_d() {
    showQR_d = !showQR_d }



</script>


<div class= "page">


													  			 <!-- Card -->

<div>
	<title>Generate Password</title>


<p class="title">Generate Password</p> 
<div class="card-1 dark glass small-shadow" >  

<div class="card-bg"> </div>


	<div class="tab" >

  <input  type="radio" class="tab__radio" name="tab" id="one"
  bind:group={manualEntry} value={false}  checked/>
  	<label for="one" class="tab__label">Random</label>
  		<div class="tab__contents"> 

  																<!-- Tab 1 -->	
  			<br>
  				
																	<!-- Slider -->
					<div class="flex " style="padding-left: 0.5ch; padding-right: 0.5ch;">
						<span>{password_length}</span>
						<span>Characters</span>
					
					</div>

					
				
					  
					<input aria-label="password length" class="slider" type="range" 
							     style="--position:{((password_length-12) / 8) * 100}%"
						 		bind:value={password_length} min="12" max="20" />


					<div  style="font-size: var(--extra-small-font);">

						 	<p class="flex-slider">
									<span> ╹ </span> <span> ╹ </span> <span> ╹ </span> <span> ╹ </span> 
									<span> ╹ </span> <span> ╹ </span> <span> ╹ </span><span> ╹ </span>
									<span> ╹ </span>
						 	</p>

						 	<p class="flex-slider">	
									<span > 12 </span> <span> 13 </span> <span> 14 </span> <span> 15 </span> 
									<span> 16 </span> <span> 17 </span> <span> 18 </span><span> 19 </span>
									<span> 20 </span>
						 	</p>

					</div>
					
					<br>

															   	<!-- Slider -->


																<!-- Toggle Group -->

					<div class="tgl-group " >

						<button name="Capitalize" class="toggle-text {capitalize_first_letter ? 'toggle-on' : ''}  " 
						on:click={f_capitalize_first_letter}>Capitalize</button>

						<button name="Numbers" class="toggle-text {add_number ? 'toggle-on' : ''} " 
						on:click={f_add_number}>Numbers</button>

						<button name="specialcharacters" class="toggle-text {add_special_char ? 'toggle-on' : ''} " 
						on:click={f_add_special_char}>!@#$%&...</button>
					 
					</div>
<br> 
<br> 
																<!-- Toggle Group -->



																		<!-- Inputs -->
			
				<p class="center" style="font-size:var(--big-font)">{password}</p>

					<div class="btn-group" style="margin-top: 4ch ">

								<button class="main drop-shadow" on:click={setManualEntryToFalse} > Regenerate </button>
	      			 <button on:click={toggleToast} name="Copy" use:copy={password}  class="main drop-shadow" > Copy
	      			  </button>     	

					</div>

  </div>

																		<!-- Tab 2 -->


  <input type="radio" class="tab__radio" name="tab" id="two"
  bind:group={manualEntry} value={true}  />
 		 <label for="two" class="tab__label">Manual</label>
 			 <div class="tab__contents"> 

 			 	<br>

					<div class="flex">
							<form autocomplete="off">
							<input type="text" autocomplete="off" class="input dark glass" name="firstname" placeholder="Password" 
							bind:value={password}>
							</form>
							 {#if password}
							 	
							 
	      			 <button on:click={toggleToast} use:copy={password}  class="main drop-shadow" > Copy </button>
	      			 {:else}

	      			 <button class="main disabled" > Copy </button>

							{/if}
					</div>


 			 </div>

  <div class="tab__indicator" /></div>
  																 <!--invisible Card -->
<br>
	  {#if password }
	  <div class="text-box">
    <p >{guess} &nbsp;</p>
    <p class={boxClass}></p>
    <p>{strength}</p>
    <p>{strength2}</p>
	  </div>
  {/if}

</div>


</div>
 																		<!--invisible  Card -->	


 																		 <!-- Second Card -->


<div>
	<title>Evaluate Password</title>

<p class="title">Encryption and Decryption</p>
<div class="card-1 dark glass small-shadow" > 
<div>
	<div class="card-bg" style="height: 18.8ch;"> </div>
	
			<form autocomplete="off" >
				
				<div class="flex spacing" >
					<input type="text" autocomplete="off" class="input dark glass kv " name="Key"
					 placeholder="Key" bind:value={Key}>
						 <span class="key-indicator">
					    {#if Key}
					      {Key_count}
					    {/if}
					   </span>
				</div>
				
					<div class="flex spacing" style="height:var(--portion);" >
					<input type="text" autocomplete="off" class="input dark glass kv " name="IV" 
					placeholder="IV" bind:value={IV}>
					<span class="key-indicator">
					    {#if IV}
					      {IV_count}
					    {/if}
					   </span>
				</div>

			</form>

</div>

<br>
	<div class="tab-2">

  <input  type="radio" class="tab__radio" name="tab-2" id="first"  checked/>
  	<label for="first" class="tab__label">Encrypt</label>
  		<div class="tab__contents"> 
  			<br>


						<label class="check">Use Password
						  <input type="checkbox" on:click={f_auto_plain} >
						  <span class="checkmark"></span>
						</label>
						{#if auto_plain == false}
							<textarea  class="txt-area dark glass" rows="2"
							 bind:value={plain_text} placeholder="Plain Text"></textarea>
							 {:else}

							 <textarea  class="txt-area dark glass" rows="2" readonly
							 value={plain_text} placeholder="Plain Text"></textarea>
						{/if}

						{#if Key && IV}
						<p class="center result" >{result_e}</p>

						{/if}

				{#if Key && IV &&
					result_e !== "IV is not 16 Characters" &&
		      result_e !== "Key is not 16 Characters" &&
		      result_e !== "Invalid Credentials"&&
		      result_e !== ""}

				<div class="btn-group  "> 
					
	      	<button on:click={toggleToast} name="Copy" use:copy={result_e}  class="main drop-shadow" > Copy </button>
					<button name="Show QR Code" class="main drop-shadow" on:click={toggleQR_e}> Show QR Code</button>
				</div>
				{:else}
				<div class="btn-group  "> 
					<button name="Copy" class="main disabled "> Copy</button>
					<button name="Show QR Code" class="main disabled "> Show QR Code</button>
				</div>

				{/if}
<div class="qr">
{#if showQR_e && plain_text && Key && IV &&
					result_e !== "IV is not 16 Characters" &&
		      result_e !== "Key is not 16 Characters" &&
		      result_e !== "Invalid Credentials"&&
		      result_e !== ""}

					<QRCodeImage class="qr" text={result_e} width={160} height={160} margin={1} />
					{/if}
 </div>			


  		</div>

  <input type="radio" class="tab__radio" name="tab-2" id="second" />
 		 <label for="second" class="tab__label">Decrypt</label>
 			 <div class="tab__contents"> 
			<br>

  			
						
							 <textarea  class="txt-area dark glass" rows="2" 
							 bind:value={cipher_text} placeholder="Cipher Text"></textarea>
						

						{#if Key && IV}
						<p class="center result" >{result_d}</p>
				
						{/if}

				{#if Key && IV &&
					result_d !== "IV is not 16 Characters" &&
		      result_d !== "Key is not 16 Characters" &&
		      result_d !== "Invalid Credentials"&&
		      result_d !== ""}

				<div class="btn-group  "> 
					
	      	<button on:click={toggleToast} name="Copy" use:copy={result_d}  class="main drop-shadow" > Copy </button>
					<button  name="Show QR Code" class="main drop-shadow" on:click={toggleQR_d}> Show QR Code</button>
				</div>
				{:else}
				<div class="btn-group  "> 
					<button name="Copy" class="main disabled "> Copy</button>
					<button name="Show QR Code" class="main disabled "> Show QR Code</button>
				</div>

				{/if}
<div class="qr">
{#if showQR_d && cipher_text && Key && IV &&
					result_e !== "IV is not 16 Characters" &&
		      result_e !== "Key is not 16 Characters" &&
		      result_e !== "Invalid Credentials"&&
		      result_e !== ""}

					<QRCodeImage class="qr" text={result_d} width={160} height={160} margin={1} />
					{/if}
 </div>			


  		

 			 </div>
				<div class="tab__indicator" /></div>

</div>



</div>
    <div class="toast dark glass" class:opentoast={isToastOpen}>
    	<span class="gg-check-o"/>
    	<span>&nbsp Copied</span>


</div>
</div>


<style>

  .key-indicator {
    position: absolute;
    right: 35px;
		top: 50%;
    transform: translateY(-50%);
    color: #777;
    pointer-events: none;
    font-size: var(--regular-font);
  }

  .result {
  	font-size:var(--big-font); 
  	margin-top: 2ch; 
  	margin-bottom: 2ch; 
  	word-wrap: normal ;
  	text-align: center;
  }



  .kv{

  	background: var(--inout-bg);
  	border: none;
  	border-radius: var(--radiu-a);
  }
  
  .kv:focus{
  	background: var(--input-bg-focus);
  }


  .box {
  	display: flex;
  	align-items: center;
    transition: width 0.5s, background-color 0.5s, background-position 0.5s ;
    border-radius: var(--radiu-a);
  	background-color: red; 
  	margin-bottom: 10px;
  	height: 0.3ch;
  	margin-top: 0.5ch;
  	background-image: linear-gradient(to right, #f21616, #f02f11, #d47a20, #719deb, #6977e3, #7643b1, #5d43b1);
  	background-clip: content-box;
  	background-size: 300% 1ch;
  }

  .box.Too-Guessable {
  	width: 36%;
  	background-position: 0%;
    
  }

  .box.Very-Guessable {
    width: 52%;
  	background-position: 16%;
  }

  .box.Somewhat-Guessable  {
    width: 68%;
  	background-position: 32%;
  }

  .box.Safely-Unguessable  {
    width: 84%;
  	background-position: 48%;
  }

  .box.Very-Unguessable  {
    width: 100%;
  	background-position: 64%;
  }


</style>