<script>
  //svelte
  import { createEventDispatcher } from "svelte";
  import { tap } from "@sveltejs/gestures";

  // Props
  export let value = "";

  // Consts
  const dispatch = createEventDispatcher();

  // Methods
  const select = num => () => (value += num);
  const clear = () => (value = "");
  const submit = event => {
    setTimeout(() => {
      dispatch("submit");
      event.stopPropagation();
    }, 10);
  };
</script>

<style>
  .keypad {
    display: grid;
    grid-template-columns: repeat(3, 5em);
    grid-template-rows: repeat(4, 3em);
    grid-gap: 0.5em;
  }

  button {
    margin: 0;
    color: var(--color-solid-2);
    touch-action: manipulation;
  }
  button:hover,
  button:focus {
    color: var(--color-solid-3);
  }
</style>

<div class="keypad">
  <button class="btn btn-clear" use:tap on:tap={select(1)}>1</button>
  <button class="btn btn-clear" use:tap on:tap={select(2)}>2</button>
  <button class="btn btn-clear" use:tap on:tap={select(3)}>3</button>
  <button class="btn btn-clear" use:tap on:tap={select(4)}>4</button>
  <button class="btn btn-clear" use:tap on:tap={select(5)}>5</button>
  <button class="btn btn-clear" use:tap on:tap={select(6)}>6</button>
  <button class="btn btn-clear" use:tap on:tap={select(7)}>7</button>
  <button class="btn btn-clear" use:tap on:tap={select(8)}>8</button>
  <button class="btn btn-clear" use:tap on:tap={select(9)}>9</button>

  <button class="btn btn-clear" disabled={!value} use:tap on:tap={clear}>
    Clear
  </button>
  <button class="btn btn-clear" use:tap on:tap={select(0)}>0</button>
  <button class="btn btn-clear" disabled={!value} on:click={submit}>
    Submit
  </button>
</div>
