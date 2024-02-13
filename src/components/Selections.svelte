<script>
  import { createEventDispatcher } from "svelte";
  import { ready } from "../store/selectionStore";
  import { apiUrl } from "../store/urlStore";

  const dispatch = createEventDispatcher();
  let apiUrlConstant = "https://opentdb.com/api.php?amount=10&type=multiple";
  let categoryId = "9";
  let difficulty = "easy";
  $: {
    let apiUrlOptions = "&category=" + categoryId + "&difficulty=" + difficulty;
    apiUrl.set(apiUrlConstant + apiUrlOptions);
  }
</script>

<div class="container">
  <div class="section category">
    <h4>Select Category</h4>
    <select bind:value={categoryId} class="select">
      <option value="9">General Knowledge</option>
      <option value="10">Books</option>
      <option value="11">Film</option>
      <option value="12">Music</option>
      <option value="14">Television</option>
      <option value="21">Sports</option>
      <option value="22">Geography</option>
      <option value="29">Comics</option>
    </select>
  </div>
  <div class="section difficulty">
    <h4>Select Difficulty</h4>
    <select bind:value={difficulty} class="select">
      <option value="easy">Easy</option>
      <option value="medium">Medium</option>
      <option value="hard">Hard</option>
    </select>
  </div>
  <button class="btn" on:click={() => dispatch("userReady")}>
    I'm Ready!🚀
  </button>
</div>

<style>
  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1rem;
    padding: 2rem;
  }
  .section {
    width: 20rem;
    height: 5rem;
    border-radius: 0.2rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 1rem;
    color: #2a2a2a;
  }
  .category {
    background-color: #e9c46a;
  }
  .difficulty {
    background-color: #f4a261;
  }
  .select {
    height: 3rem;
    font-size: 1.2rem;
    color: #2a2a2a;
    font-weight: 800;
    border-radius: 0.5rem;
    margin-top: 1rem;
    text-align: center;
  }
  .btn {
    background-color: #2a9d8f;
    color: #edede9;
    width: 22rem;
    height: 2rem;
    font-size: 1.8rem;
    font-weight: 600;
    height: 4rem;
    border-radius: 0.2rem;
    border: none;
    cursor: pointer;
  }
</style>
