<script lang="ts">

	import { title } from '$lib/titleStore';


  let isDrawerOpen = false;
  function toggleDrawer() {
    isDrawerOpen = !isDrawerOpen;  
   
  }

  

  let rotate = false;
  function rotateLines() {
    rotate = !rotate;
  }

</script>




<div class="fixed-top dark glass flex-nav" >

  <div style="margin-inline: calc((var(--portion) - var(--small-clickable)) / 4 ); margin-right: auto;"> 
    <div style=" font-size:var(--big-font);" >{$title}</div></div>




  <div class="box">
	       <button aria-label="Menu Drawer" class="menu" on:click={rotateLines} on:click={toggleDrawer} >
  		      <div class="line line1" class:rotate={rotate}></div>
 		        <div class="line line2" class:rotate={rotate}></div>
	       </button>
  </div>

    
</div>
    <div class="drawer dark glass" class:open={isDrawerOpen}>
      
       <br>
      <a  href="/" on:click={toggleDrawer} on:click={rotateLines}><button name="Home" class="box-slim" class:rotate={rotate} >Home</button></a>
    
      <a href="/qrcode/" on:click={toggleDrawer} on:click={rotateLines} ><button name="Generate QR Code" class:rotate={rotate} class="box-slim">Generate QR Code</button></a>


      <a href="/about/" on:click={toggleDrawer} on:click={rotateLines} ><button name="About" class=" box-slim" class:rotate={rotate} >About</button></a>


       <input aria-label="theme toggle" class="theme-toggle box-slim" class:rotate={rotate} type="checkbox" id="theme-toggle" name="theme" style="margin-bottom: 8ch; margin-top: auto;"> 
      
     
	
</div>




<style>

@layer layer-2 {

/*.box{
  width: var(--portion);
  height: var(--portion);

}*/


.box-slim{
  width: 200px;
  height: 25px;
  vertical-align: center;
  background: transparent;
  border: none;
  cursor: pointer;
  text-align: start;
  color: var(--accent-color);
  font-size: var(--regular-font);
  font-family: inherit;
  opacity: 0.1;
  transform: translateX(-50px);
  



}


a {
  text-decoration: none; 
  height: 25px;
  margin:10px var(--portion); 
  margin: 100px;

  
}




}

</style>