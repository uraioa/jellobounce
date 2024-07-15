<script lang="ts">
    import MainButton from "./buttons/MainButton.svelte";
    import ButtonContainer from "../common/buttons/ButtonContainer.svelte";
    import IconTextButton from "../common/buttons/IconTextButton.svelte";
    import IconButton from "../common/buttons/IconButton.svelte";
    import Account from "../common/header/Account.svelte";
    import {fade} from "svelte/transition";
    import {
        browse,
        exitClient,
        getClientUpdate,
        openScreen,
        toggleBackgroundShaderEnabled
    } from "../../../integration/rest";
    import Menu from "../common/Menu.svelte";
    import {fly} from "svelte/transition";
    import {onMount} from "svelte";
    import {notification} from "../common/header/notification_store";

    let regularButtonsShown = true;
    let clientButtonsShown = false;

    onMount(() => {
        setTimeout(async () => {
            const update = await getClientUpdate();

            if (update.updateAvailable) {
                notification.set({
                    title: `LiquidBounce ${update.newestVersion?.clientVersion} has been released!`,
                    message: `Download it from liquidbounce.net!`,
                    error: false,
                    delay: 99999999
                });
            }
        }, 2000);
    });

    function toggleButtons() {
        if (clientButtonsShown) {
            clientButtonsShown = false;
            setTimeout(() => {
                regularButtonsShown = true;
            }, 750);
        } else {
            regularButtonsShown = false;
            setTimeout(() => {
                clientButtonsShown = true;
            }, 750);
        }
    }

    function currentTime(): string {
        const now = new Date();
        const hours = now.getHours();
        const minutes = now.getMinutes();
            return `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}`;
}
</script>

<Menu>
    <div class="content">
        <div class="clock" transition:fly|global={{duration: 500, y: -100}}>{currentTime()}</div>
        <div class="account" transition:fade|global={{duration: 500}}><Account/></div>
        <div class="main-buttons">
            {#if regularButtonsShown}
                <MainButton title="Singleplayer" icon="singleplayer" index={0}
                            on:click={() => openScreen("singleplayer")}/>

                <MainButton title="Multiplayer" icon="multiplayer" let:parentHovered
                            on:click={() => openScreen("multiplayer")} index={1}>
                </MainButton>
                <MainButton title="Configure" icon="options" on:click={toggleButtons} index={2}/>
            {:else if clientButtonsShown}
                <MainButton title="Proxies" icon="proxymanager" on:click={() => openScreen("proxymanager")}
                            index={0}/>
                <MainButton title="ClickGUI" icon="clickgui" on:click={() => openScreen("clickgui")} index={1}/>
                    <MainButton title="Options" icon="options" on:click={() => openScreen("options")} index={2}/>
                <!-- <MainButton title="Scripts" icon="scripts" index={2}/> -->
                <MainButton title="Back" icon="back-large" on:click={toggleButtons} index={3}/>
            {/if}
        </div>

        <div class="additional-buttons" transition:fly|global={{duration: 500, y: 100}}>
            <ButtonContainer>
                <IconTextButton title="Exit" on:click={exitClient}/>
                <IconTextButton title="Toggle Shader"
                                on:click={toggleBackgroundShaderEnabled}/>
            </ButtonContainer>
        </div>

        <div class="social-buttons" transition:fly|global={{duration: 500, y: 100}}>
            <ButtonContainer>
                <IconButton title="Forum" icon="nodebb" on:click={() => browse("MAINTAINER_FORUM")}/>
                <IconButton title="GitHub" icon="github" on:click={() => browse("MAINTAINER_GITHUB")}/>
                <IconButton title="Guilded" icon="guilded" on:click={() => browse("MAINTAINER_GUILDED")}/>
                <IconButton title="Discord" icon="discord" on:click={() => browse("MAINTAINER_DISCORD")}/>
                <IconButton title="Twitter" icon="twitter" on:click={() => browse("MAINTAINER_TWITTER")}/>
                <IconButton title="YouTube" icon="youtube" on:click={() => browse("MAINTAINER_YOUTUBE")}/>
                <IconTextButton title="liquidbounce.net"
                                on:click={() => browse("CLIENT_WEBSITE")}/>
            </ButtonContainer>
        </div>
    </div>
</Menu>

<style>

    .clock {
        font-family: inter;
        color: white;
        opacity: 0.8;
        font-size: 250px;
        font-weight: 800;
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
        z-index: 1;
    }

    .account {
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
        bottom: 50px;
    }

    .content {
        flex: 1;
        display: grid;
        grid-template-areas:
            "a ."
            "b c";
        grid-template-rows: 1fr max-content;
        grid-template-columns: 1fr max-content;
    }

    .main-buttons {
        display: flex;
        flex-direction: row;
        row-gap: 25px;
        grid-area: a;
        position: absolute;
        bottom: 25px;
        left: 50.5%;
        transform: translateX(-50%);
    }

    .additional-buttons {
        grid-area: b;
    }

    .social-buttons {
        grid-area: c;
    }
</style>