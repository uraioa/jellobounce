<script lang="ts">
    import {fade} from "svelte/transition";
</script>

<div class="bottom-button-wrapper" transition:fade|global={{duration: 650}}>
    <slot/>
</div>

<style lang="scss">
  .bottom-button-wrapper {
    display: flex;
    justify-content: space-between;
  }
</style>