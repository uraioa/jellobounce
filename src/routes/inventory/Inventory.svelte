<script lang="ts">
    import {fade} from "svelte/transition";
</script>

<div class="logo" transition:fade={{duration: 200}}>jellobounce</div>
<div class="shaderfix" transition:fade={{duration: 200}}></div>

<style lang="scss">
    @import "../../colors.scss";

    .logo {
        position: absolute;
        left: 15px;
        top: 15px;
        font-family: Borel;
        color: rgba(white, 1);
        font-size: 50px;
        text-shadow: 0px 0px 10px rgba(black, 0.3);
        z-index: 1;
        text-align: center;
    }

    .shaderfix {
        position: absolute;
        background-color: rgba(black, 0.1);
        height: 100vw;
        width: 100vw;
        z-index: -1;
    }
</style>