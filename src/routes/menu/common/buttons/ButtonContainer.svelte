<div class="button-container">
    <slot />
</div>

<style lang="scss">
    @import "../../../../colors.scss";

    .button-container {
      background: none;
      width: max-content;
      display: flex;
      column-gap: 1px;
    }
</style>