<script lang="ts">
    import {fade} from "svelte/transition";
</script>

<div class="option-bar" transition:fade|global={{duration: 650}}>
    <slot />
</div>

<style lang="scss">
    @import "../../../../colors";

    .option-bar {
      background-color: rgba($background-color, 0.68);
      padding: 15px 30px;
      display: flex;
      border-radius: 12px;
      align-items: center;
      column-gap: 30px;
      margin-bottom: 25px;
       
    }
</style>