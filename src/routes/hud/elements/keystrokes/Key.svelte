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
    background-color: rgba($background-color, $transparency);
    color: $text-color;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 12px;
    font-size: 17px;
    font-weight: 500;
    transition: ease background-color .3s;
    position: relative;
    text-align: center;
    font-family: sf-pro;
    box-shadow: 0px 0px 10px rgba($shadow-color, 0.5);
    border: solid 1px $border-thing;

    &.active {
      background-color: rgba($accent-color, 0.7);
      border-radius: 12px;
      scale: 95%;
      align-self: center;
      font-size: 17px;
    }
  }
</style>