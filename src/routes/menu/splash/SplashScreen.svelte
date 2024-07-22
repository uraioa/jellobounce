<script lang="ts">
    import {fade} from "svelte/transition";
</script>

<div class="background" 
    in:fade|global={{duration: 100}}
    out:fade|global={{duration: 500}}
></div>
<img class="logo" src="img/menu/icon-liquidbounce.svg" alt="logo" 
    in:fade|global={{duration: 100}}
    out:fade|global={{duration: 500}}
>

<style lang="scss">

  .background {
    background-color: black;
    width: 7050px;
    height: 4050px;
  }
  
  .logo {
    position: fixed;
    top: 50%;
    left: 51%;
    transform: translateX(-50%);
    scale: 300%;
  }
</style>