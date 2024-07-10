<script lang="ts">
    import Account from "./Account.svelte";
    import Notifications from "./Notifications.svelte";
</script>

<div class="skibidi">
  <div class="logo">jellobounce</div>
</div>

<div class="header">
  <img src="a" alt="">

    <Notifications/>

    <Account/>
</div>

<style lang="scss">

  .skibidi {
    font-family: borel;
    color: white;
    text-shadow: 0px 0px 10px rgba(black, 0.3);
    font-size: 80px;
  }

  .header {
    position: absolute;
    justify-content: space-between;
    margin-bottom: 25px;
    align-items: center;
    right: 25px;
    top: 25px;
  }
</style>