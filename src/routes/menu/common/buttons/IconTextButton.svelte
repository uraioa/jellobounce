<script lang="ts">
    import {createEventDispatcher} from "svelte";

    export let title: string;
    export let disabled = false;

    const dispatch = createEventDispatcher();
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->
<button class="icon-text-button" on:click={() => dispatch("click")} {disabled}>
    <div class="icon">
    </div>
    <div class="title">{title}</div>
</button>

<style lang="scss">
    @import "../../../../colors.scss";

    .icon-text-button {
      display: flex;
      border: none;
      border-radius: 12px;
      align-items: center;
      overflow: hidden;
      background: linear-gradient(to left, rgba($background-color, 0.5) 50%, $accent-color 50%);
      background-size: 200% 100%;
      background-position: right bottom;
      will-change: background-position;
      transition: ease opacity .15s, background-position .15s ease-out;
      font-family: sf-pro;
      height: 58px;

      &:not([disabled]):hover {
        &:hover {
          background-position: left bottom;
          cursor: pointer;
        }
      }

      &[disabled] {
        opacity: .6;
      }
    }

    .title {
      font-size: 20px;
      font-weight: 400;
      color: $text-color;
      padding: 0 25px;
    }
</style>