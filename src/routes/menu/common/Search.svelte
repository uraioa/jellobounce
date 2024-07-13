<script lang="ts">
    import {createEventDispatcher} from "svelte";

    let value = "";

    const dispatch = createEventDispatcher<{
        search: { query: string }
    }>();
</script>

<input class="search" type="text" placeholder="Search..." bind:value={value}
       on:input={() => dispatch("search", {query: value})}>

<style lang="scss">
  @import "../../../colors.scss";

  .search {
    background-color: rgba($background-color, .36);
    border: none;
    color: $text-color;
    font-family: "sf-pro", sans-serif;
    font-size: 20px;
    border-radius: 12px;
    background-image: url("/img/menu/icon-search.svg");
    background-repeat: no-repeat;
    background-position: 20px center;
    padding: 20px 20px 20px 60px;
    flex: 1;
    box-shadow: 0px 0px 10px rgba($shadow-color, 0.5);
    margin-left: -14px;
  }
</style>