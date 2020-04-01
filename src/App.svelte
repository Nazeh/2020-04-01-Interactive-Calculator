<script>
  import Chart from 'chart.js';
  import { onMount } from 'svelte';

  let ctx;
  let growthRate = 1.1;
  let startWith = 1;
  const yearsNo = 30;
  $: years = [startWith];
  let wealth = [1];

  $: {
    for (let year = 1; year <= yearsNo; year += 1) {
      years = [...years, years.slice(-1)[0] + 1];
      wealth = [...wealth, wealth.slice(-1)[0] * growthRate];
    }
  }

  const createChart = (data, xLabels) => {
    ctx = document.getElementById('myChart').getContext('2d');

    new Chart(ctx, {
      type: 'bar',
      data: {
        labels: xLabels,
        datasets: [
          {
            label: 'Accumulated',
            data,
          },
        ],
      },
    });
  };

  onMount(() => createChart(wealth, years));
</script>

<style>

</style>

<h1>Compound growth calculator!</h1>
<canvas id="myChart" width="400" height="400" />
<input type="range" bind:value={startWith} />
<input type="range" bind:value={growthRate} />
