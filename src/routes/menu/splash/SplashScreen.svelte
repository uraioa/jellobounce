<script lang="ts">
    import {fade} from "svelte/transition";
</script>

<div class="logo" out:fade|global={{duration: 500}}>jellobounce</div>

<style lang="scss">
  .logo {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-family: borel;
    color: white;
    text-shadow: 0px 0px 10px rgba(black, 0.3);
    font-size: 50px;
    }
</style>