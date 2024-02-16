<script>
  import Score from "./Score.svelte";
  import { score, questionNumber } from "../store/scoreStore";
  import { ready } from "../store/selectionStore";
  import { onMount } from "svelte";

  export let questions = [];

  let selectedOption;
  let wrong;
  let correct;
  let options = [];
  let disableNext;

  onMount(() => {
    selectedOption = "";
    wrong = false;
    correct = false;
    disableNext = false;

    () => {
      selectedOption = "";
      wrong = false;
      correct = false;
      disableNext = false;
    };
  });

  $: {
    options = [
      ...questions[$questionNumber].incorrect_answers,
      questions[$questionNumber].correct_answer,
    ].sort(() => 0.5 - Math.random());
  }

  const handleCheckAnswer = () => {
    if (questions[$questionNumber].correct_answer === selectedOption) {
      wrong = false;
      correct = true;
      score.update((val) => val + 1);
    } else {
      wrong = true;
    }
  };

  const handleNextQuestion = () => {
    selectedOption = "";
    wrong = false;
    correct = false;

    if (questions.length - 1 !== $questionNumber) {
      questionNumber.update((val) => val + 1);
    } else {
      disableNext = true;
    }
  };

  const handleReset = () => {
    ready.set(false);
    score.set(0);
  };
</script>

<div class="container">
  <div class="question">
    <p>{@html questions[$questionNumber].question}</p>
    {#each options as option}
      <div class="option">
        <input
          class="radio-type"
          type="radio"
          bind:group={selectedOption}
          value={option}
        />
        {@html option}
      </div>
    {/each}
    <div class="buttons">
      <button
        on:click={handleCheckAnswer}
        disabled={selectedOption ? false : true}
        style={selectedOption ? "" : "background-color: grey"}
        >Check Answer {wrong ? "🤕👎🏻" : correct ? "🤓👍🏻" : "🤔"}</button
      >
      {#if !disableNext}
        <button on:click={handleNextQuestion}> Next Question 👉🏻 </button>
      {:else}
        <button on:click={handleReset} style="background-color: #E76F51;">
          Reset Quiz 🛟</button
        >
      {/if}
    </div>
  </div>
  <Score />
</div>

<style>
  .container {
    width: 60rem;
    padding: 2rem;
    display: flex;
  }

  .question {
    width: 80%;
    background-color: #e9c46a;
    padding: 2rem;
    border-top-left-radius: 0.2rem;
    border-bottom-left-radius: 0.2rem;
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
    background-color: #ffffff;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .radio-type {
    width: 1.5rem;
    height: 1.5rem;
  }

  .buttons {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1rem;
    margin-top: 1rem;
  }

  button {
    color: #2a2a2a;
    width: 15rem;
    height: 3rem;
    font-size: 1.2rem;
    font-weight: 600;
    border: none;
    border-radius: 0.2rem;
    cursor: pointer;
    background-color: #2a9d8f;
  }
</style>
