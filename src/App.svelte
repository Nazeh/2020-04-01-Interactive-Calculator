<script>
  import MyChart from "./components/Chart.svelte";

  let growthRate = 1.1;
  let startWith = 1;
  let wealth;
  const yearsNo = 30;

  $: {
    wealth = [startWith];
    for (let year = 1; year <= yearsNo; year += 1) {
      wealth = [...wealth, wealth.slice(-1)[0] * growthRate];
    }
  }
</script>

<MyChart data={wealth} />
<label>
  initial amount
  <input type="range" bind:value={startWith} />
</label>
<label>
  Growth rate
  <input type="range" bind:value={growthRate} />
</label>
