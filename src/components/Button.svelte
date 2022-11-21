<script>
  export let style = "primary";
  export let type = "button";
  export let disabled = false;
</script>

<button {type} {disabled} class={style}>
  <slot />
</button>

<style>
  button {
    background-color: #ff6a95;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 5px;
    cursor: pointer;
    width: 100px;
  }

  button:hover {
    background-color: #ff6a94cd;
    transform: scale(1.02);
  }

  button:disabled {
    background-color: #cccccc;
    cursor: not-allowed;
  }

  button:disabled:hover {
    transform: scale(1);
    opacity: 1;
  }

  .input-group {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 20px 0;
  }

  input {
    width: 100%;
    padding: 10px;
    border: 1px solid #eee;
    border-radius: 5px;
    margin-bottom: 10px;
  }

  .primary {
    background-color: #202142;
  }

  .secondary {
    background-color: #ff6a95;
  }
</style>
