<script>
  import Cell from "./Cell.svelte";

  export let KanjiSet;
  export let AxisSize;
</script>

<section style={`--axis-size: ${AxisSize}`}>
  {#each KanjiSet as character}
    <Cell character={character.kanji} />
  {/each}
</section>

<style>
  section {
    --axis-size: 1;
    --cell-size: 100px;
    --gap: 1rem;
    --size: calc(
      var(--cell-size) * var(--axis-size) + var(--gap) * (var(--axis-size) - 1)
    );

    display: grid;
    grid-gap: 1rem;
    grid-template-columns: repeat(var(--axis-size), 1fr);
    grid-template-rows: repeat(var(--axis-size), 1fr);
    width: var(--size);
    height: var(--size);
  }
</style>
