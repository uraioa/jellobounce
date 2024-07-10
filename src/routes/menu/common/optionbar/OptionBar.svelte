<script lang="ts">
    import {fade} from "svelte/transition";
</script>

<div class="option-bar" transition:fade|global={{duration: 650}}>
    <slot />
</div>

<style lang="scss">
    @import "../../../../colors";

    .option-bar {
      background-color: rgba($background-color, $transparency);
      padding: 15px 30px;
      display: flex;
      border-radius: 12px;
      align-items: center;
      column-gap: 30px;
      margin-bottom: 10px;
      box-shadow: 0px 0px 10px rgba($background-color, 0.5);
      scale: 80%;
      margin-left: -12%;
      margin-right: -12%;
      font-family: urbanist-variable;
      font-size: 16px;
    }
</style>