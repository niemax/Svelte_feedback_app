<script>
  import { FeedbackStore } from "../stores";
  import Card from "./Card.svelte";
  import Dialog from "./Modal.svelte";
  export let item;

  let modalOpen = false;

  const handleDelete = (id) => {
    FeedbackStore.update((currentItems) => {
      return currentItems.filter((item) => item.id !== id);
    });
  };
</script>

<Card>
  <div class="num-display">{item.rating}</div>
  <button on:click={() => (modalOpen = true)}>
    <p>Open Dialog</p>
  </button>
  <button class="close" on:click={() => handleDelete(item.id)}>X</button>
  <p class="text-display">
    {item.text}
  </p>
</Card>

<Dialog open={modalOpen} />

<style>
  .num-display {
    position: absolute;
    top: -10px;
    left: -10px;
    width: 50px;
    height: 50px;
    background: #ff6a95;
    color: #fff;
    border: 1px #eee solid;
    border-radius: 50%;
    padding: 10px;
    text-align: center;
    font-size: 19px;
  }
  .close {
    position: absolute;
    top: 10px;
    right: 20px;
    cursor: pointer;
    background: none;
    border: none;
    color: black;
  }
  .text-display {
    color: black;
  }
</style>
