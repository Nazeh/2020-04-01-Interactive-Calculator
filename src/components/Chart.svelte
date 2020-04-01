<script>
  import Chart from "chart.js";

  import { afterUpdate } from "svelte";
  export let data = [];
  $: xLabels = data.map((d, i) => i);

  let ctx;
  let myChart;

  const createChart = (data, xLabels) => {
    ctx = document.getElementById("myChart").getContext("2d");
    if (myChart) myChart.destroy();

    myChart = new Chart(ctx, {
      type: "bar",
      data: {
        labels: xLabels,
        datasets: [
          {
            label: "Accumulated",
            data
          }
        ]
      }
    });
  };

  afterUpdate(() => createChart(data, xLabels));
</script>

<style>
  .chart-container {
    width: 400px;
  }
</style>

<h1>Compound growth calculator!</h1>
<div class="chart-container">
  <canvas id="myChart" width="400" height="400" />
</div>
