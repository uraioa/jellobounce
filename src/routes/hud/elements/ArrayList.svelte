<script lang="ts">
    import {onMount} from "svelte";
    import type {Module} from "../../../integration/types";
    import {getModules} from "../../../integration/rest";
    import {listen} from "../../../integration/ws";
    import {getTextWidth} from "../../../integration/text_measurement";
    import {flip} from "svelte/animate";
    import {fly} from "svelte/transition";
    import {convertToSpacedString, spaceSeperatedNames} from "../../../theme/theme_config";
    import {backOut} from "svelte/easing";

    let enabledModules: Module[] = [];

    async function updateEnabledModules() {
        enabledModules = (await getModules())
            .filter((m) => m.enabled && !m.hidden)
            .sort(
                (a, b) =>
                    getTextWidth($spaceSeperatedNames ? convertToSpacedString(b.name) : b.name, "500 14px urbanist-variable") -
                    getTextWidth($spaceSeperatedNames ? convertToSpacedString(a.name) : a.name, "500 14px urbanist-variable"),
            );
    }

    spaceSeperatedNames.subscribe(async () => {
        await updateEnabledModules();
    });

    onMount(async () => {
        await updateEnabledModules();
    });

    listen("toggleModule", async () => {
        await updateEnabledModules();
    });

    listen("refreshArrayList", async () => {
        await updateEnabledModules();
    });
</script>

<div class="arraylist">
    {#each enabledModules as { name } (name)}
        <div class="module" animate:flip={{duration: 200}} in:fly={{x: 50, duration: 200}} out:fly={{x: 50, duration: 200}}>
            {$spaceSeperatedNames ? convertToSpacedString(name) : name}
        </div>
    {/each}
</div>

<style lang="scss">
    @import "../../../colors.scss";

    .arraylist {
        //position: fixed;
        //top: 0;
        //right: 0;
    }

    .module {
        background-color: rgba($background-color, $transparency);
        color: $text-color;
        font-size: 15px;
        font-family: sf-pro;
        padding: 5px 8px;
        width: max-content;
        font-weight: 400;
        margin-left: auto;
        box-shadow: -5px 0px 10px rgba(black, 0.27), 5px 0px 10px rgba(black, 0.27);

    }

    .module:first-child {
        box-shadow: 0px -5px 10px rgba(black, 0.17), -5px 0px 10px rgba(black, 0.17), 5px 0px 10px rgba(black, 0.17);
    }

    .module:last-child {
        box-shadow: 0px 5px 10px rgba(black, 0.17), -5px 0px 10px rgba(black, 0.17), 5px 0px 10px rgba(black, 0.17);
    }
</style>
