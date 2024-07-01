<script lang="ts">
    import {listen} from "../../../../integration/ws";
    import type {KeyEvent} from "../../../../integration/events";
    import type {MinecraftKeybind} from "../../../../integration/types";

    export let gridArea: string;
    export let key: MinecraftKeybind | undefined;

    let active = false;

    listen("key", (e: KeyEvent) => {
        if (e.key.name !== key?.key.translationKey) {
            return;
        }

        active = e.action === 1 || e.action === 2;
    });
</script>

<div class="key" style="grid-area: {gridArea};" class:active>
    {key?.key.localized ?? "???"}
</div>

<style lang="scss">
  @import "../../../../colors.scss";

  .key {
    height: 50px;
    background-color: rgba($keystrokes-base-color, $transparency);
    color: $keystrokes-text-color;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 12px;
    font-size: 17px;
    font-weight: 500;
    transition: ease background-color .3s;
    position: relative;
    background-color: rgba(black, 0.6);
    text-align: center;
    font-family: Inter;
    box-shadow: 0px 0px 20px rgba(black, 0.6);
    border: solid 1px $border-thing;

    &.active {
      background-color: rgba($accent-color, 0.9);
      border-radius: 12px;
      scale: 95%;
      align-self: center;
      font-size: 17px;
    }
  }
</style>