<script>
  import Selections from "./Selections.svelte";
  import Questions from "./Questions.svelte";

  // use a store for ready 👇🏻
  let ready = false;
</script>

<div class="quiz">
  {#if ready}
    <Questions />
  {:else}
    <Selections />
  {/if}
</div>

<style>
  .quiz {
    background-color: #edede9;
    height: calc(100vh - 10rem);
    width: 100%;
  }
</style>
