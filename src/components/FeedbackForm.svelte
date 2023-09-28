<script>
  import { v4 as uuidv4 } from "uuid";
  import { FeedbackStore } from "../stores";
  import Card from "./Card.svelte";
  import Button from "./Button.svelte";
  import RatingSelect from "./RatingSelect.svelte";

  let text = "";
  let rating = 10;
  let btnDisabled = true;
  let errorMessage;
  const minTextLength = 1;

  const handleInput = () => {
    if (text.trim().length <= minTextLength) {
      errorMessage = `Text must be at least ${minTextLength} characters`;
    } else {
      errorMessage = null;
      btnDisabled = false;
    }
  };

  const handleRatingSelect = (e) => (rating = e.detail);

  const handleSubmit = () => {
    if (text.trim().length > minTextLength) {
      const newFeedback = {
        id: uuidv4(),
        text,
        rating: +rating,
      };

      FeedbackStore.update((currentItems) => {
        return [...currentItems, newFeedback];
      });
      text = "";
    }
  };
</script>

<Card>
  <header>
    <h2>How would you rate your service with us?</h2>
  </header>
  <form on:submit|preventDefault={handleSubmit}>
    <RatingSelect on:rating-select={handleRatingSelect} />
    <div class="input-group">
      <input
        type="text"
        bind:value={text}
        on:input={handleInput}
        placeholder="Tell us something that keeps you coming back"
      />
      <Button disabled={btnDisabled} type="submit">Send</Button>
    </div>
    {#if errorMessage}
      <div class="message">{errorMessage}</div>
    {/if}
  </form>
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
    color: black;
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
