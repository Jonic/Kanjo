<script>
  export let KanjiAll;

  let character;
  let validKeyCodes = [13, 32];

  const keyPressHandlder = (event) =>
    validKeyCodes.includes(event.keyCode) && newKanji();

  const newKanji = () => {
    character = KanjiAll[Math.floor(Math.random() * KanjiAll.length)];
    KanjiAll = KanjiAll.filter((item) => item !== character);
  };

  newKanji();
</script>

<svelte:window on:keydown={keyPressHandlder} />

<div on:click={newKanji}>
  <strong>
    {#if character}
      {character.kun_readings.join(" / ")}
      /
      {character.on_readings.join(" / ")}
    {:else}
      Game Over
    {/if}
  </strong>

  {#if KanjiAll.length}
    <p>Remaining Kanji:</p>

    <ul>
      {#each KanjiAll as listEntry}
        <li>{listEntry.kanji}</li>
      {/each}
    </ul>
  {/if}
</div>

<style>
  div {
    max-width: 50ch;
    text-align: center;
    user-select: none;
  }

  p {
    margin-bottom: 1rem;
  }

  strong {
    font-size: 3rem;
  }

  ul {
    display: flex;
    flex-wrap: wrap;
    margin: 0 0 1rem;
    max-width: 50ch;
    padding: 0;
  }

  li {
    list-style: none;
    margin: 0.25rem;
  }
</style>
