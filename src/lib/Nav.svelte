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


<body  id ="display-drawer">
<div class="card">

<div class="fixed-top dark glass flex" style="font-weight: bold;">

  <div> &nbsp &nbsp {$title}</div>


  <div class="box">
      <a aria-label="Menu Drawer" href="#/" on:click={toggleDrawer}>
	       <button name="Menu Drawer" class="menu" on:click={rotateLines}>
  		      <div class="line line1" class:rotate={rotate}></div>
 		        <div class="line line2" class:rotate={rotate}></div>
	       </button>
      </a>
  </div>

    
</div>
    <div class="drawer dark glass" class:open={isDrawerOpen}>
      
       
      <a  href="/#/" on:click={toggleDrawer} on:click={rotateLines}><button name="Home" class="box-slim">&nbsp Home</button></a>
    
      <a href="/qrcode#/" on:click={toggleDrawer} on:click={rotateLines} ><button name="Generate QR Code" class="box-slim">&nbsp Generate QR Code</button></a>


      <a href="/about#/" on:click={toggleDrawer} on:click={rotateLines} ><button name="About" class="box-slim">&nbsp About</button></a>
      
     
	
</div>
</div>
</body>


<style>

@layer layer-2 {
.box{
  width: 50px;
  height: 50px;



}

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




}

a {
  text-decoration: none; 
  height: 25px;
  margin:10px 50px; 
  margin: 100px;



}


}

</style>