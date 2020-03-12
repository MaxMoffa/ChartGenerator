<canvas height="270px" id="graph_container"></canvas>

<script>
  import { title_stored, label_stored, data_stored } from '../stored_data.js';
  import {onMount} from 'svelte'
  import Chart from 'chart.js';

  let ctx = null;
  let myChart = null;

  title_stored.subscribe(value => {
    if(myChart !== null){
      myChart.options.title.fontStyle = "normal";
      myChart.options.title.fontFamily = "Arial";
      myChart.options.title.text = value;
      myChart.options.title.display = (value !== "");
      window.setTimeout(() => {myChart.update();}, 0);
    }
  });

  label_stored.subscribe(value => {
    if(myChart !== null){
      myChart.data.labels = value;
      window.setTimeout(() => {myChart.update();}, 0);
    }
  });

  data_stored.subscribe(value => {
    if(myChart !== null){
      myChart.data.datasets = value;
      window.setTimeout(() => {myChart.update();}, 0);
    }
  });

  onMount(() => {
    let ctx = document.getElementById('graph_container').getContext('2d');
    myChart = new Chart(ctx, {
      type: 'bar',
      data: {
        labels: [],
        datasets: []
      },
      options: {
        maintainAspectRatio: false,
          scales: {
              yAxes: [{
                  ticks: {
                      beginAtZero: true
                  }
              }]
          },
      }
    });
  });
</script>
