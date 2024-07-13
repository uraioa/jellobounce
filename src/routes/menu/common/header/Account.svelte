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

        <div class="icon">
    </button>
</div>

<style lang="scss">
  @import "../../../../colors";

  .account {
    background-color: rgba($background-color, $transparency);
    padding: 15px 15px;
    border-radius: 12px;
    align-items: center;
    display: grid;
    grid-template-areas:
        "a b c"
        "a d c";
    grid-template-columns: max-content 1fr max-content;
    column-gap: 15px;
    border: solid 1px $border-thing;
    font-family: sf-pro;
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
    font-size: 20px;
    grid-area: b;
    align-self: flex-end;
  }

  .account-type {
    font-weight: 400;
    font-size: 20px;
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
    height: max-content;
    cursor: pointer;
    width: 68px;
    height: 68px;
    border-radius: 50%;
  }
</style>
