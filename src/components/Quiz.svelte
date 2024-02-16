<script>
  import Selections from "./Selections.svelte";
  import Questions from "./Questions.svelte";
  import { ready } from "../store/selectionStore";
  import { apiUrl } from "../store/urlStore";

  let questions = [];

  const getQuizQuestions = async () => {
    const res = await fetch($apiUrl);
    const data = await res.json();
    if (data && data.results) {
      questions = [...data?.results];
      ready.update((val) => !val);
    }
  };
</script>

<div class="quiz">
  {#if $ready}
    <Questions {questions} />
  {:else}
    <Selections on:userReady={getQuizQuestions} />
  {/if}
</div>

<style>
  .quiz {
    height: calc(100vh - 12rem);
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
</style>
