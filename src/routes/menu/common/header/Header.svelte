<script lang="ts">
    import Account from "./Account.svelte";
    import Notifications from "./Notifications.svelte";

    function currentTime(): string {
  const now = new Date();
  const hours = now.getHours();
  const minutes = now.getMinutes();
  return `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}`;
}
</script>
<div class="header">
    <div class="clock">{currentTime()}</div>
      <div class="notifications">
        <Notifications />
      </div>
            <Account/>
</div>

<style lang="scss">
  @import "../../../../colors.scss";

  .clock {
    font-family: sf-pro;
    color: rgba(white, 0.8);
    font-size: 250px;
    font-weight: 600;
    position: relative;
    left: 50%;
    transform: translateX(-50%);
    z-index: 1;
  }
  
  .header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 60px;
    align-items: center;
    z-index: 1;

    .notifications {
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
    }
  }
</style>