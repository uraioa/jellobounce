<script lang="ts">
    import {fly} from "svelte/transition";
    import {backInOut} from "svelte/easing";
    import {onMount} from 'svelte';
    import {fade} from 'svelte/transition';

    let visible = true;

    onMount(() => {
        const timer = setTimeout(() => {
            visible = false;
        }, 0);

    return () => clearTimeout(timer);
});
</script>

    {#if visible}
        <div class="fade" transition:fade={{duration: 1000}}></div>
    {/if}

<div class="watermark" transition:fly|global={{duration: 500, y: -50, easing: backInOut}}>jello</div>
<div class="shaderfix"></div>

<style lang="scss">
    .watermark {
        //position: fixed;
        //top: 15px;
        //left: 15px;
        font-family: Borel;
        color: rgba(white, 1);
        font-size: 50px;
        z-index: 1;
        text-shadow: 0px 0px 10px rgba(black, 0.3);
    }

    .fade {
        position: absolute;
        top: -15px;
        left: -15px;
        background-color: black;
        width: 7050px;
        height: 4050px;
        z-index: -3;
    }

    .shaderfix {
        top: -15px;
        left: -15px;
        position: absolute;
        background-color: rgba(black, 0.1);
        width: 7050px;
        height: 4050px;
        z-index: -2;
    }
</style>
