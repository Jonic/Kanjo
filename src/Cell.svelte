<script>
  import { beforeUpdate } from "svelte";

  export let character;

  let active;

  const handleClick = () => (active = !active);

  const valueCheck = () => {
    return {
      update() {
        active = false;
      },
    };
  };
</script>

<div class:active on:click={handleClick} use:valueCheck={character}>
  {character}
</div>

<style>
  div {
    --background-color: white;
    --border-color: grey;
    --opacity: 1;
    --scale: 1;

    align-items: center;
    background-color: var(--background-color);
    border-color: var(--border-color);
    border-style: solid;
    border-width: 3px;
    cursor: pointer;
    display: flex;
    font-size: 3rem;
    height: 100px;
    justify-content: center;
    line-height: 1;
    opacity: var(--opacity);
    scale: var(--scale);
    user-select: none;
    width: 100px;
  }

  div.active {
    --background-color: lightgrey;
    --border-color: purple;
    --opacity: 0.5;
    --scale: 0.95;
  }
</style>
