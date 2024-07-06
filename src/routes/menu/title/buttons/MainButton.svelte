<script lang="ts">
    import {fade} from "svelte/transition";
    import {createEventDispatcher} from "svelte";
    import {backIn, backOut} from "svelte/easing";

    export let title: string;
    export let icon: string;
    export let index: number;

    let hovered = false;

    const dispatch = createEventDispatcher();
</script>

<!-- svelte-ignore a11y-no-static-element-interactions -->
<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="main-button" on:mouseenter={() => hovered = true} on:mouseleave={() => hovered = false}
     on:click={() => dispatch("click")} out:fade|global={{duration: 350, delay: index * 100, easing: backIn}}
     in:fade|global={{duration: 350, delay: index * 100, easing: backOut}}>
    <div class="icon">
        {#if !hovered}
            <img transition:fade={{duration: 200}} src="img/menu/icon-{icon}.svg" alt={icon}>
        {:else}
            <img transition:fade={{duration: 200}} src="img/menu/icon-{icon}-hover.svg" alt={icon}>
        {/if}
    </div>

    <div class="title">{title}</div>

    <div class="wrapped-content">
        <slot parentHovered={hovered}/>
    </div>
</div>

<style lang="scss">
  @import "../../../../colors.scss";

  .main-button {
    padding: 15px;
    width: 500px;
    position: relative;
    display: grid;
    grid-template-columns: max-content 1fr max-content;
    align-items: center;
    cursor: pointer;
    will-change: background-position;
    scale: 90%;
    background-color: rgba($background-color, $transparency);
    margin: -10px;
    border-radius: 12px;
    background-size: 200% 100%;
    column-gap: 15px;
     

    &:hover {

      .icon {
        background-color: $text-color;
      }
    }
  }

  .icon {
    background-color: $accent-color;
    width: 90px;
    height: 90px;
    border-radius: 50%;
    transition: ease background-color 0.2s;
    position: relative;

    img {
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
    }
  }

  .title {
    font-size: 26px;
    color: $text-color;
    font-weight: 600;
  }
</style>
