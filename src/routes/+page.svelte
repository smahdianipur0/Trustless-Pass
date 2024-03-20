<script lang="ts">

//House keeping
  import { title } from '$lib/titleStore'; title.set('Home');
	import { copy }  from 'svelte-copy';


	//slider
 	$: sliderStyle = `linear-gradient(to right, rgba(250, 250, 250,0.7) 0%, 
 	rgba(250, 250, 250,0.6)
 	${((password_length-12) / 8) * 100}%, rgba(70, 70, 70,0.4) 
 	${((password_length-12) / 8) * 100}%, rgba(70, 70, 70,0.5) 100%)`;


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


	import { times_two } from "$lib/pkg/rust_lib";
	let a = 16;
	$: b = times_two(a).toString();


  //Rust Functions
  import { encrypt }                      from "$lib/pkg/rust_lib";
  import { decrypt }                      from "$lib/pkg/rust_lib";
  import { count_characters }             from "$lib/pkg/rust_lib";
  import { generate_password }            from "$lib/pkg/rust_lib";
  import { calculate_password_strength }  from "$lib/pkg/rust_lib";
  import { calculate_password_strength2 } from "$lib/pkg/rust_lib";
  import { guessable }                    from "$lib/pkg/rust_lib";


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
  let password = '';

  $: if (manualEntry) {
  password = ''; 
  } else {
    password = generate_password(password_length, add_special_char, add_number, capitalize_first_letter);
  }

  $: guess = guessable(password);
  $: strength = calculate_password_strength(password);
  $: strength2 = calculate_password_strength2(password);


	let Key = '';
  $: Key_count = count_characters(Key);

  let IV = '';
  $: IV_count = count_characters(IV);

  let plain_text = '';
  let auto_plain = false;
  function f_auto_plain() {
    auto_plain = !auto_plain; } 

  

  $: if (auto_plain) {
  plain_text = password; 
  } else {
    plain_text = '';
  }


  $: result_e = encrypt(Key,IV,plain_text);
  let cipher_text = '';
  let result_d = '';
  $: result_d = decrypt(Key,IV,cipher_text);





</script>

<body  id ="display-toast">
<div class="card">
<div class= "page">


													  			 <!-- Card -->

<div class="card-2">
<div class="card-1 dark glass small-shadow" >  

	<div class="tab">

  <input  type="radio" class="tab__radio" name="tab" id="one"
  bind:group={manualEntry} value={false}  checked/>
  	<label for="one" class="tab__label">Random</label>
  		<div class="tab__contents"> 

  																<!-- Tab 1 -->	
  			<br>
  				
																	<!-- Slider -->

					<div class="flex">
					<div class="length">Length: {password_length} </div> 
					<div>
							<input class="slider" type="range" style="--sliderBackground: {sliderStyle}"	
						 		bind:value={password_length} min="12" max="20" />

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
					</div>

															   	<!-- Slider -->


																<!-- Toggle Group -->

					<div class="tgl-group " >

						<button class="toggle-text {capitalize_first_letter ? 'toggle-on' : ''}  " 
						on:click={f_capitalize_first_letter}>Capitalize</button>

						<button class="toggle-text {add_number ? 'toggle-on' : ''} " 
						on:click={f_add_number}>Numbers</button>

						<button class="toggle-text {add_special_char ? 'toggle-on' : ''} " 
						on:click={f_add_special_char}>!@#$%&...</button>
					 
					</div>
<br> 
																<!-- Toggle Group -->



																		<!-- Inputs -->
			<div class="flex">

				<form autocomplete="off">
						<input type="text" autocomplete="off" class="input dark glass " readonly value="{password}">	
				</form>
					<a href="/#" on:click={toggleToast}>
	      			 <button use:copy={password}  class="main" > Copy </button>
					</a>
<br>

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
							<input type="text" autocomplete="off" class="input dark glass" name="firstname" placeholder="password" 
							bind:value={password}>
							</form>
							<a href="/#" on:click={toggleToast}>
	      			 <button use:copy={password}  class="main" > Copy </button>
					</a>
							<br>
					</div>


 			 </div>

  <div class="tab__indicator" /></div>
  																 <!-- Card -->
<br>
	  {#if password }
    <p style = " font-size: 14px;" >{guess}</p>
    <p style = " font-size: 14px;">{strength}</p>
    <p style = " font-size: 14px;">{strength2}</p>
  {/if}

</div>

</div>
 																		<!-- Card -->	

<div class="card-1 dark glass small-shadow" > 
<div class="card-2">
	
			<form autocomplete="off">
				
				<div class="flex">
					<input type="text" autocomplete="off" class="input dark glass" name="Key"
					 placeholder="Key" bind:value={Key}>
						 <span class="key-indicator">
					    {#if Key}
					      {Key_count}
					    {/if}
					   </span>
				</div>
				
					<div class="flex">
					<input type="text" autocomplete="off" class="input dark glass" name="IV" 
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
  	<label for="first" class="tab__label">first</label>
  		<div class="tab__contents"> 
  			<br>


						<label class="check">Use Password
						  <input type="checkbox" on:click={f_auto_plain} >
						  <span class="checkmark"></span>
						</label>
						{#if auto_plain == false}
							<textarea  class="txt-area dark glass" rows="2"
							 bind:value={plain_text} placeholder="Plain Text"></textarea>
						{/if}

						{#if Key && IV}
				<textarea  class="txt-area dark glass" rows="2" readonly
				bind:value={result_e}></textarea>
						{/if}

				<div class="btn-group"> 
					<button class="main "> click</button>
					<button class="main "> click</button>

				</div>


  			


  		</div>

  <input type="radio" class="tab__radio" name="tab-2" id="second" />
 		 <label for="second" class="tab__label">second</label>
 			 <div class="tab__contents"> 
			<br>

  			<textarea  class="txt-area dark glass" rows="2" readonly>how you doing?
				</textarea>

 			 </div>
				<div class="tab__indicator" /></div>
	



</div>
</div>



</div>
    <div class="toast dark glass" class:opentoast={isToastOpen}> Copied 

</div>
</body>


<style>



.flex-slider {
	font-size: 10px;
	padding: 0 2.5px;
}

.length{
	height:30px;
	vertical-align: text-top;
}



/*.input{	
	width: auto;

}*/



.row-box{
	height: 40px;
	display: flex;
	justify-content: space-between;
}

  .key-indicator {
    position: absolute;
    right: 15px;
		top: 25px;
    transform: translateY(-50%);
    color: #777;
    pointer-events: none;
  }

</style>