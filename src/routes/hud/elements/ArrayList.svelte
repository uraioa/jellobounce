<script lang="ts">
    import {onMount, tick} from "svelte";
    import type {Module} from "../../../integration/types";
    import {getModules} from "../../../integration/rest";
    import {listen} from "../../../integration/ws";
    import {getTextWidth} from "../../../integration/text_measurement";
    import {flip} from "svelte/animate";
    import {fly} from "svelte/transition";
    import {convertToSpacedString, spaceSeperatedNames} from "../../../theme/theme_config";

    let enabledModules: Module[] = [];

    async function updateEnabledModules() {
        const modules = await getModules();
        const visibleModules = modules.filter(m => m.enabled && !m.hidden);

        const modulesWithWidths = visibleModules.map(module => {
                let formattedName = $spaceSeperatedNames ? convertToSpacedString(module.name) : module.name;
                let fullName = module.tag == null ? formattedName : formattedName + " " + module.tag;

                return {
                    ...module,
                    width: getTextWidth(fullName, "500 14px Inter")
                };
            }
        );

        modulesWithWidths.sort((a, b) => b.width - a.width);

        enabledModules = modulesWithWidths;
        await tick();
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
    {#each enabledModules as {name, tag} (name)}
        <div class="module" animate:flip={{duration: 200}} in:fly={{x: 50, duration: 200}} out:fly={{x: 50, duration: 200}}>
            {$spaceSeperatedNames ? convertToSpacedString(name) : name}
            {#if tag}
                <span class="tag"> {tag}</span>
            {/if}
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
        font-family: "sf-pro";
        padding: 5px 8px;
        width: max-content;
        font-weight: 400;
        margin-left: auto;
        box-shadow: -5px 0px 10px rgba(black, 0.27), 5px 0px 10px rgba(black, 0.27);
    }

    .tag {
        color: $arraylist-tag-color;
    }

    .module:first-child {
        box-shadow: 0px -5px 10px rgba(black, 0.17), -5px 0px 10px rgba(black, 0.17), 5px 0px 10px rgba(black, 0.17);
    }

    .module:last-child {
        box-shadow: 0px 5px 10px rgba(black, 0.17), -5px 0px 10px rgba(black, 0.17), 5px 0px 10px rgba(black, 0.17);
    }
</style>
