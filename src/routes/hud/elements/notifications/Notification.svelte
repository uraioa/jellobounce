<script lang="ts">
    export let title: string;
    export let message: string;
    export let severity: string;
</script>

<div class="notification">
    <div class="icon {severity.toString().toLowerCase()}"/>
    <div class="title">{title}</div>
    <div class="message">{message}</div>
</div>

<style lang="scss">
  @import "../../../../colors.scss";

  .notification {
    display: grid;
    grid-template-areas:
            "a b"
            "a c";
    grid-template-columns: max-content 1fr;
    column-gap: 10px;
    background: rgba(black, $transparency);
    border-radius: 12px;
    min-width: 298px;
    overflow: hidden;
    padding: 10px;
    margin-bottom: 10px;
    box-shadow: 0px 0px 10px rgba(black, 0.4);
    border: solid 1px $border-thing;
  }

  .icon {
    height: 40px;
    width: 40px;
    background-position: center;
    background-repeat: no-repeat;
    border-radius: 100px;
    grid-area: a;
    transition: background-color 0.2s;
    position: relative;

    &.success {
      background-color: #4dac6800;
      background-image: url("/img/hud/notification/icon-success.svg");
    }

    &.error {
      background-color: #fc413000;
      background-image: url("/img/hud/notification/icon-error.svg");
    }

    &.info {
      background-color: #4677ff00;
      background-image: url("/img/hud/notification/icon-info.svg");
    }

    &.disabled,
    &.enabled {
      &::after {
        content: "";
        position: absolute;
        height: 10px;
        width: 10px;
        border-radius: 100px;
        top: 50%;
        transform: translate(-50%, -50%);
        background: white;
        transition: all 0.2s ease-out;
      }

      background-image: url("/img/hud/notification/icon-toggle.svg");
    }

    &.enabled {
      background-color: #4dac6800;

      &::after {
        left: 62%;
      }
    }

    &.disabled {
      background-color: #fc413000;

      &::after {
        left: 38%;
      }
    }
  }

  .title {
    grid-area: b;
    font-size: 14px;
    color: white;
    font-weight: 600;
  }

  .message {
    grid-area: c;
    font-size: 12px;
    color: #cbd1e3;
  }
</style>
