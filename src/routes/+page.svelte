<script lang="ts">

  //House keeping
  import { title }          from '$lib/titleStore'; title.set('Home');
	import { copy }           from 'svelte-copy';

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

	//slider
 	$: sliderStyle = `linear-gradient(to right, rgba(250, 250, 250,0.7) 0%, 
 	rgba(250, 250, 250,0.6)
 	${((a-12) / 8) * 100}%, rgba(70, 70, 70,0.4) 
 	${((a-12) / 8) * 100}%, rgba(70, 70, 70,0.5) 100%)`;


	//toggle
  let toggle = false;
  function toggleBackground() {
    toggle = !toggle;
  }


</script>

<body  id ="display-toast">
<div class="card">




<div class= "page">


													  			 <!-- Card -->

<div class="card-2">
<div class="card-1 dark glass small-shadow" >  

	<div class="tab">

  <input  type="radio" class="tab__radio" name="tab" id="one"  checked/>
  	<label for="one" class="tab__label">One</label>
  		<div class="tab__contents"> 

  																<!-- Tab 1 -->	
  			<br>
  				
																	<!-- Slider -->

					<div class="flex">
					<div class="length">Length: {a} </div> 
					<div>
							<input class="slider" type="range" style="--sliderBackground: {sliderStyle}"	
						 		bind:value={a} min="12" max="20" />

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

						<button class="toggle-text {toggle ? 'toggle-on' : ''}  " 
						on:click={toggleBackground}>Toggle</button>

						<button class="toggle-text {toggle ? 'toggle-on' : ''} " 
						on:click={toggleBackground}>Toggle</button>

						<button class="toggle-text {toggle ? 'toggle-on' : ''} " 
						on:click={toggleBackground}>Toggle</button>
					  
					</div>

																<!-- Toggle Group -->

<br>
{#if toggle}
<p> toggle on </p>
{:else}
toggle off
{/if}
<br>

																		<!-- Inputs -->
			<div class="flex">

				<form autocomplete="off">
						<input type="text" autocomplete="off" class="input dark glass " readonly value="{a} times two equals to  {times_two(a)}">	
				</form>
					<a href="/#" on:click={toggleToast}>
	      			 <button use:copy={b}  class="main" > Copy </button>
					</a>


			</div>

  </div>
																		<!-- Tab 2 -->
  <input type="radio" class="tab__radio" name="tab" id="two" />
 		 <label for="two" class="tab__label">Two</label>
 			 <div class="tab__contents"> 

 			 	<br>

					<div class="flex">
							<form autocomplete="off">
							<input type="text" autocomplete="off" class="input dark glass" name="firstname" placeholder="Your name..">
							</form>
							<button  class="main small-shadow "> Hello ! </button>
							<br>
					</div>


 			 </div>

  <div class="tab__indicator" /></div>
  																 <!-- Card -->
<br>
	<p> With the number of users, devices and programs in the modern enterprise increasing along with the amount of data -- much of which is sensitive or confidential -- cybersecurity is more important than ever. But the volume and sophistication of cyberattackers and attack techniques compound the problem even further.
	</p>

</div>

</div>
 																		<!-- Card -->	

<div class="card-1 dark glass small-shadow" > 
<div class="card-2">
	
			<form autocomplete="off">
				<div class="row-box">
					<input type="text" autocomplete="off" class="input dark glass" name="friendname" placeholder="firiend name..">
				</div>
					<div class="row-box">
					<input type="text" autocomplete="off" class="input dark glass" name="schoolnmae" placeholder="school name..">
				</div>
			</form>

</div>

<br>
	<div class="tab-2">

  <input  type="radio" class="tab__radio" name="tab-2" id="first"  checked/>
  	<label for="first" class="tab__label">first</label>
  		<div class="tab__contents"> 
  			<br>


						<label class="check">One
						  <input type="checkbox" >
						  <span class="checkmark"></span>
						</label>

				<textarea  class="txt-area dark glass" rows="2">Hi
				</textarea>
				<textarea  class="txt-area dark glass" rows="2" readonly>Hi
				</textarea>


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

.input:read-only{
	width: auto;

	
}

.input{
	
/*	padding: 5px;*/
	padding: var(--default-padding);


}

.row-box{
	height: 40px;
}



</style>