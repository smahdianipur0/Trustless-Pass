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

<div class="fixed-top dark glass flex">

  <div> &nbsp &nbsp {$title}</div>


  <div class="box">
      <a href="#/" on:click={toggleDrawer}>
	       <button class="menu" on:click={rotateLines}>
  		      <div class="line line1" class:rotate={rotate}></div>
 		        <div class="line line2" class:rotate={rotate}></div>
	       </button>
      </a>
  </div>

    
</div>
    <div class="drawer dark glass" class:open={isDrawerOpen}>
      
       
      <a href="/#/" on:click={toggleDrawer} on:click={rotateLines}><button class="box-slim">Home</button></a>
    
      <a href="/qrcode#/" on:click={toggleDrawer} on:click={rotateLines} ><button class="box-slim">Generate QR Code</button></a>


      <a href="/about#/" on:click={toggleDrawer} on:click={rotateLines} ><button class="box-slim">About</button></a>
      
     
	
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
  height: 20px;
  vertical-align: center;
  background: transparent;
  border: none;
  cursor: pointer;
  text-align: start;

}

a {
  text-decoration: none; 
  height: 20px;
  margin:10px 50px; 
  color: var(--accent-color);

}


}

</style>