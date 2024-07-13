<script lang="ts">
    import Account from "./Account.svelte";
    import Notifications from "./Notifications.svelte";
</script>

<div class="header">
    <div class="logo">jellobounce</div>

    <Notifications />

    <Account/>
</div>

<style lang="scss">

  .logo {
    font-family: Borel;
    color: rgba(white, 1);
    font-size: 85px;
    text-shadow: 0px 0px 10px rgba(black, 0.2);
  }

  .header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 60px;
    align-items: center;
  }
</style>