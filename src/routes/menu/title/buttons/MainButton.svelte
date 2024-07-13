<script lang="ts">
    import {fade, fly} from "svelte/transition";
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
     on:click={() => dispatch("click")} out:fly|global={{duration: 400, x: -500, delay: index * 100, easing: backIn}}
     in:fly|global={{duration: 400, x: -500, delay: index * 100, easing: backOut}}>
    <div class="icon">
        {#if !hovered}
            <img transition:fade={{duration: 150}} src="img/menu/icon-{icon}.svg" alt={icon}>
        {:else}
            <img transition:fade={{duration: 150}} src="img/menu/icon-{icon}-hover.svg" alt={icon}>
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
    background-color: rgba($background-color, $transparency);
    width: 500px;
    padding: 17px 24px;
    display: grid;
    grid-template-columns: max-content 1fr max-content;
    align-items: center;
    cursor: pointer;
    border-radius: 12px;
    column-gap: 25px;
    background: linear-gradient(to left, rgba($background-color, $transparency) 50%, $accent-color 50%);
    background-size: 200% 100%;
    background-position: right bottom;
    will-change: background-position;
    transition: background-position .16s ease;
    font-family: sf-pro;
    font-weight: normal;
    border: solid 1px $border-thing;

    &:hover {
      background-position: left bottom;

      .icon {
        background-color: $text-color;
      }
    }
  }

  .icon {
    background-color: rgba($accent-color, 0.7);
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
  }
</style>
