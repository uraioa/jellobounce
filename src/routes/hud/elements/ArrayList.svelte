<script lang="ts">
    import {onMount, tick} from "svelte";
    import type {Module} from "../../../integration/types";
    import {getModules} from "../../../integration/rest";
    import {listen} from "../../../integration/ws";
    import {getTextWidth} from "../../../integration/text_measurement";
    import {flip} from "svelte/animate";
    import {fly} from "svelte/transition";
    import {convertToSpacedString, spaceSeperatedNames} from "../../../theme/theme_config";
    import {getPrefix} from "../../../theme/arraylist";

    let enabledModules: Module[] = [];
    let prefixs = new Map();

    async function updateEnabledModules() {
        const modules = await getModules();
        const visibleModules = modules.filter(m => m.enabled && !m.hidden);

        for (let module of visibleModules) {
        const updatePrefix = await getPrefix(module.name);
        
        if (!prefixs.has(module.name) || prefixs.get(module.name) !== updatePrefix) {
            prefixs.set(module.name, updatePrefix);
        }
    }

        const modulesWithWidths = visibleModules.map(module => ({
            ...module,
            width: getTextWidth($spaceSeperatedNames ? (convertToSpacedString(module.name) + prefixs.get(module.name)) : (module.name + prefixs.get(module.name)), "400 15px sf-pro")
        }));

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
    {#each enabledModules as { name } (name)}
        <div class="module" animate:flip={{ duration: 200 }} in:fly={{ x: 50, duration: 200 }} out:fly={{ x: 50, duration: 200 }}>
            {$spaceSeperatedNames ? convertToSpacedString(name) : name} <h class="prefix">{prefixs.get(name)}</h> 
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

    .prefix {
        color: #AAAAAA;
    }

    .module:first-child {
        box-shadow: 0px -5px 10px rgba(black, 0.17), -5px 0px 10px rgba(black, 0.17), 5px 0px 10px rgba(black, 0.17);
    }

    .module:last-child {
        box-shadow: 0px 5px 10px rgba(black, 0.17), -5px 0px 10px rgba(black, 0.17), 5px 0px 10px rgba(black, 0.17);
    }
</style>
