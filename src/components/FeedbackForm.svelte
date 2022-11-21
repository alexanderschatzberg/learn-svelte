<script>
  import { v4 as uuid } from "uuid";
  import Card from "./Card.svelte";
  import Button from "./Button.svelte";
  import RatingSelect from "./RatingSelect.svelte";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  let text = "";
  let rating = null;
  let btnDisabled = true;
  let message = "";

  const handleInput = () => {
    btnDisabled = text.length <= 10;
    if (btnDisabled) {
      message = "Please enter at least 10 characters";
    } else {
      message = null;
    }
  };

  const handleSelect = (e) => {
    rating = e.detail;
  };

  const handleSubmit = () => {
    const newFeedback = {
      id: uuid(),
      text,
      rating: parseInt(rating),
    };
    dispatch("add-feedback", newFeedback);
    text = "";
  };
</script>

<Card>
  <header>
    <h2>How would you rate your experience?</h2>
  </header>
  <RatingSelect on:rating-select={handleSelect} />
  <form on:submit|preventDefault={handleSubmit}>
    <div class="input-group">
      <input
        on:input={handleInput}
        type="text"
        bind:value={text}
        placeholder="Tell us something about the buisness"
      />
      <Button disabled={btnDisabled} type="submit">Submit</Button>
    </div>
  </form>
  {#if message}
    <p class="message">{message}</p>
  {/if}
</Card>

<style>
  header {
    max-width: 400px;
    margin: auto;
  }

  header h2 {
    font-size: 22px;
    font-weight: 600;
    text-align: center;
  }

  .input-group {
    display: flex;
    flex-direction: row;
    border: 1px solid #ccc;
    padding: 8px 10px;
    border-radius: 8px;
    margin-top: 15px;
  }

  input {
    flex-grow: 2;
    border: none;
    font-size: 16px;
  }

  input:focus {
    outline: none;
  }

  .message {
    padding-top: 10px;
    text-align: center;
    color: rebeccapurple;
  }
</style>
