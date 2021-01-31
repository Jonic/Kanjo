<script>
  export let caller;
  export let sizes;
  export let setSize;
  export let resetGame;
  export let toggleCaller;

  let sizeLabels = {
    sm: "Small",
    md: "Medium",
    lg: "Large",
    xl: "Extra Large",
  };
</script>

<nav>
  <ul>
    <li><button on:click={resetGame}>Reset</button></li>
    <li>
      <button on:click={toggleCaller}>Caller: {caller ? "On" : "Off"}</button>
    </li>

    {#each Object.keys(sizes) as currentSize}
      <li>
        <button on:click={setSize(currentSize)}
          >Grid: {sizeLabels[currentSize]}</button
        >
      </li>
    {/each}
  </ul>
</nav>

<style>
  nav {
    margin: 1rem 0 2rem;
  }

  ul {
    display: flex;
    justify-content: center;
    margin: 0;
    padding: 0;
  }

  li {
    list-style: none;
    margin: 0 1rem;
  }

  button {
  }
</style>
