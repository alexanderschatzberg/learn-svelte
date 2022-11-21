<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  export let item;
  import Card from "./Card.svelte";

  const handleDelete = (itemID) => {
    dispatch("delete-feedback", itemID); //Set bubbles up
  };
</script>

<Card>
  <div class="num-display">
    {item.rating}
  </div>
  <button
    class="close"
    on:click={() => {
      handleDelete(item.id);
    }}>X</button
  >
  <div class="text-display">
    {item.text}
  </div>
</Card>

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
    top: 7px;
    right: 10px;
    cursor: pointer;
    background: none;
    border: none;
  }
</style>
