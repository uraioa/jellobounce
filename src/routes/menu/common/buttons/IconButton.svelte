<script lang="ts">
    import ToolTip from "../ToolTip.svelte";
    import {createEventDispatcher} from "svelte";

    export let title: string;
    export let icon: string;

    const dispatch = createEventDispatcher();
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->
<div class="icon-button" on:click={() => dispatch("click")}>
    <ToolTip text={title}/>

    <div class="icon">
        <img src="img/menu/icon-{icon}.svg" alt={icon}>
    </div>
</div>

<style lang="scss">
  @import "../../../../colors.scss";
  
  .icon-button {
    position: relative;
  }

  .icon {
    height: 58px;
    width: 58px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    background-color: rgba($background-color, $transparency);
    box-shadow: 0px 0px 10px rgba($background-color, 0.5);
    border-radius: 12px;
    margin-right: 10px;
  }
</style>