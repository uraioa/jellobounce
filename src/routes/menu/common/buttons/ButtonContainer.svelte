<div class="button-container">
    <slot />
</div>

<style lang="scss">
    @import "../../../../colors.scss";

    .button-container {
      background: none;
      display: flex;
      column-gap: 15px;
      padding: 15px;
      align-items: center;
      width: max-content;
    }
</style>