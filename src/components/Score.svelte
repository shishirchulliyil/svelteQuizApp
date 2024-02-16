<script>
  import { score } from "../store/scoreStore";
  import { ready } from "../store/selectionStore";

  const handleReset = () => {
    ready.set(false);
    score.set(0);
  };
</script>

<div class="container">
  <button class="reset" on:click={handleReset}>Reset Quiz 🛟</button>
  {#if $score > 8}
    <div class="myscore">
      <p class="label">YOU</p>
      <p class="label">ARE</p>
      <p class="label">A</p>
      <p class="label">WINNER</p>
      <p class="label">🥳</p>
      <p class="score">{$score}</p>
    </div>
  {:else}
    <div class="myscore">
      <p class="label">YOUR</p>
      <p class="label">SCORE</p>
      <p class="score">{$score}</p>
    </div>
  {/if}
</div>

<style>
  .container {
    width: 20%;
    border-bottom-right-radius: 0.2rem;
    background-color: #e76f51;
    border-top-right-radius: 0.2rem;
  }

  .reset {
    background-color: #f4a261;
    border-top-right-radius: 0.2rem;
    padding: 1rem;
    cursor: pointer;
    font-size: 1.2rem;
    text-align: center;
    font-weight: 600;
    color: #2a2a2a;
    border: none;
    width: 100%;
  }

  .myscore {
    display: flex;
    padding: 2rem;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    margin-top: 2rem;
  }

  .label {
    font-size: 2rem;
    font-weight: 100;
    color: #ffffff;
  }

  .score {
    font-size: 10rem;
    font-weight: 900;
    color: #ffffff;
  }
</style>
