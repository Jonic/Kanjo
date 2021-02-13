<script>
  import KanjiData from "./data/kanji-rich";

  import Caller from "./Caller.svelte";
  import Grid from "./Grid.svelte";
  import Menu from "./Menu.svelte";

  let params = new URLSearchParams(window.location.search);

  let sizes = {
    sm: 9,
    md: 16,
    lg: 25,
    xl: 36,
  };

  let caller = false;
  let initialized = false;
  let size;

  let AxisSize;
  let KanjiAll;
  let KanjiCount;
  let KanjiSet;
  let title = "カンジョ！";

  const newKanjiSet = (KanjiAll, KanjiCount) => {
    const set = KanjiAll.slice();

    for (let i = set.length - 1; i > 0; i--) {
      const rand = Math.floor(Math.random() * (i + 1));
      [set[i], set[rand]] = [set[rand], set[i]];
    }

    return set.slice(0, KanjiCount);
  };

  const resetGame = () => {
    updateParams();

    caller = params.get("caller") === "true";
    size = params.get("size") || "sm";

    KanjiCount = sizes[size];

    AxisSize = Math.sqrt(KanjiCount);
    KanjiAll = [].concat(...KanjiData.slice());
    KanjiSet = newKanjiSet(KanjiAll, KanjiCount);

    initialized = true;
  };

  const setSize = (newSize) => {
    params.set("size", newSize);
    resetGame();
  };

  const toggleCaller = () => {
    params.set("caller", !caller);
    resetGame();
  };

  const updateParams = () => {
    if (params instanceof URLSearchParams) {
      const paramsString = params.toString();
      params = paramsString ? `?${paramsString}` : window.location.pathname;
    }

    window.history.replaceState({}, document.title, params);
    params = new URLSearchParams(window.location.search);
  };

  resetGame();
</script>

<svelte:head>
  <title>{title}</title>
</svelte:head>

{#if initialized}
  <h1>{title}</h1>

  <Menu {caller} {resetGame} {setSize} {sizes} {toggleCaller} />

  <main>
    <Grid {KanjiSet} {AxisSize} />

    {#if caller}
      <Caller {KanjiAll} />
    {/if}
  </main>
{/if}

<style>
  h1 {
    font-size: 3rem;
    margin-top: 1rem;
    text-align: center;
  }

  main {
    align-items: top;
    display: flex;
    gap: 2rem;
    justify-content: center;
    margin: 0 auto;
    max-width: 1200px;
    min-height: 100vh;
  }
</style>
