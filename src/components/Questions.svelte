<script>
  import { onMount } from "svelte";

  export let questions = [];
  let questionNumber = 0;
  let selectedOption = "";
  let options = [];
  $: {
    options = [
      ...questions[questionNumber].incorrect_answers,
      questions[questionNumber].correct_answer,
    ].sort(() => 0.5 - Math.random());
  }

  $: {
    console.log("selected :", selectedOption);
  }
</script>

<div class="container">
  <div class="question">
    <p>{questions[0].question}</p>
    {#each options as option}
      <div class="option">
        <input
          class="radio-type"
          type="radio"
          bind:group={selectedOption}
          value={option}
        />
        {option}
      </div>
    {/each}
  </div>
</div>

<style>
  .container {
    width: 60rem;
    padding: 2rem;
  }

  .question {
    background-color: #f4a261;
    padding: 2rem;
    border-radius: 0.2rem;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    font-size: 1.2rem;
    font-weight: 700;
    color: #2a2a2a;
  }

  .option {
    border-radius: 0.2rem;
    padding: 1rem;
    background-color: #edede9;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .radio-type {
    width: 1.5rem;
    height: 1.5rem;
  }

  .radio-type:checked {
    color: #e9c46a;
  }
</style>
