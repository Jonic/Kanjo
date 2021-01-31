<script>
  import { beforeUpdate } from "svelte";

  export let character;

  let active;

  const handleClick = () => (active = !active);

  const valueCheck = (_, character) => {
    return {
      update(character) {
        console.log(character);
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
    --border-color: grey;

    align-items: center;
    border-color: var(--border-color);
    border-style: solid;
    border-width: 3px;
    cursor: pointer;
    display: flex;
    font-size: 3rem;
    height: 100px;
    justify-content: center;
    line-height: 1;
    user-select: none;
    width: 100px;
  }

  div.active {
    --border-color: red;
  }
</style>
