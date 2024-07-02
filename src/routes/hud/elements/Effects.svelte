<script lang="ts">
    import {listen} from "../../../integration/ws";
    import type {ClientPlayerDataEvent} from "../../../integration/events";
    import type {StatusEffect} from "../../../integration/types";
    import {fade} from "svelte/transition";

    let effects: StatusEffect[] = [];

    listen("clientPlayerData", (event: ClientPlayerDataEvent) => {
        effects = event.playerData.effects;
    });

    function formatTime(duration: number): string {
        return new Date(((duration / 20) | 0) * 1000).toISOString().substring(14, 19);
    }

    function convertToRoman(n: number): string {
        switch (n) {
            case 0: return "I";
            case 1: return "II";
            case 2: return "III";
            case 3: return "IV";
            case 4: return "V";
            case 5: return "VI";
            case 6: return "VII";
            case 7: return "VIII";
            case 8: return "IX";
            case 9: return "X";
            default: return "X+";
        }
    }
</script>

<div class="effects">
    {#each effects as e}
        <div class="effect" transition:fade|global={{duration: 200}}>
            <span class="name" style="color: {'#' + e.color.toString(16)}">{e.localizedName} {convertToRoman(e.amplifier)}:</span>
            <span class="duration">{formatTime(e.duration)}</span>
        </div>
    {/each}
</div>

<style lang="scss">
  @import "../../../colors.scss";

  .effect {
    font-weight: 500;
    font-size: 14px;
    text-align: left;
    background-color: rgba(black, $transparency);
    padding: 5px 8px;
    box-shadow: 0px 0px 20px rgba(black, 0.6);

    .duration {
      color: white;
    }
  }

  .effect:first-child {
    border-top-left-radius: 12px;
    border-top-right-radius: 12px;
  }

  .effect:last-child {
    border-bottom-left-radius: 12px;
    border-bottom-right-radius: 12px;
  }
</style>