<script lang="ts">
    import ToolTip from "../ToolTip.svelte";
    import {getSession, openScreen} from "../../../../integration/rest";
    import {onMount} from "svelte";
    import {listen} from "../../../../integration/ws";

    let username = "";
    let avatar = "";
    let premium = true;

    async function refreshSession() {
        const session = await getSession();
        username = session.username;
        avatar = session.avatar;
        premium = session.premium;
    }

    onMount(async () => {
        await refreshSession();
    });

    listen("session", async () => {
        await refreshSession();
    });
</script>

<div class="account">
    <object data={avatar} type="image/png" class="avatar" aria-label="avatar">
        <img src="img/steve.png" alt=avatar class="avatar">
    </object>
    <div class="username">{username}</div>
    <div class="account-type">
        {#if premium}
            <span class="premium">Online</span>
        {:else}
            <span class="offline">Offline</span>
        {/if}
    </div>
    <button class="button-change-account" type="button" on:click={() => openScreen("altmanager")}>
        <ToolTip text="Change account"/>

        <img class="icon" src="a" alt="">
    </button>
</div>

<style lang="scss">
  @import "../../../../colors";

  .account {
    background-color: rgba($background-color, $transparency);
    padding: 15px 15px;
    padding-right: 15px;
    border-radius: 12px;
    align-items: center;
    display: grid;
    grid-template-areas:
        "a b c"
        "a d c";
    grid-template-columns: max-content 1fr max-content;
    column-gap: 15px;
    box-shadow: 0px 0px 10px rgba(black, 0.5);
    width: 300px;
    font-family: urbanist-variable;
    scale: 80%;
  }

  .avatar {
    height: 68px;
    width: 68px;
    border-radius: 50%;
    grid-area: a;
  }

  .username {
    font-weight: 600;
    color: $text-color;
    font-size: 25px;
    grid-area: b;
    align-self: flex-end;
  }

  .account-type {
    font-weight: 500;
    font-size: 22px;
    grid-area: d;
    align-self: flex-start;

    .premium {
      color: $menu-account-premium-color;
    }

    .offline {
      color: $text-dimmed-color;
    }
  }

  .button-change-account {
    background-color: transparent;
    border: none;
    grid-area: a;
    position: relative;
    cursor: pointer;
    width: 68px;
    height: 68px;
    border-radius: 50%;
  }
</style>
