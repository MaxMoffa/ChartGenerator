<script>
import {onMount} from 'svelte';
import Button from "../Components/Button.svelte";

export let title = "";
export let label = null;
export let data = null;
export let ctx = null;
let width = 1280;
let height = 720;
let extension = "jpg";
let chart = null

onMount(() => {
  chart = new Chart(document.querySelector('#canvas_generator').getContext('2d'), {
    type: 'bar',
    data: {
      labels: label,
      datasets: data
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      devicePixelRatio: 1,
      title:{
        fontStyle: "normal",
        fontFamily: "Arial",
        text: title,
        display: (title !== ""),
      },
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

function download() {
  if (chart !== null) {
    let image = document.querySelector("#canvas_generator").toDataURL("image/" + extension);
    let anchor = document.createElement('a');
    anchor.setAttribute('download', (title ? title : "chart_" + new Date().getTime()) + '.' + extension);
    anchor.setAttribute('href', image);
    anchor.click();
  }
}

function close() {
  ctx.$destroy();
}
</script>

<main>
<div class="body">
<div class="title">Esporta il grafico</div>
<div>
<label for="width">Larghezza (in pixel)</label>
<input id="width" type="number" placeholder="Larghezza" bind:value={width}>
</div>
<div>
<label for="height">Altezza (in pixel)</label>
<input id="height" type="number" placeholder="Altezza" bind:value={height}>
</div>
<div>
<label for="extension">Estensione</label>
<select id="extension" bind:value={extension}>
<option value="jpg">.jpg</option>
<option value="png">.png</option>
<!-- <option value="svg">.svg</option> -->
</select>
</div>
<Button text="Download" on:click={download}/>
<Button text="Chiudi" on:click={close} backgroundColor="#512da8"/>
</div>
</main>

<div class="chartGenerator" style="position: relative; height:{height}px !important; width:{width}px !important">
<canvas style="width: {width}px !important; height: {height}px !important;" id="canvas_generator"></canvas>
</div>

<style>
main{
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;

  overflow: hidden;
  z-index: 10;
  background-color: rgba(255, 255, 255);
}

.body{
  width: 100%;
  max-width: 400px;
  height: auto;
  margin: 0 auto;
}

.body div{
  margin: 18px 0;
  margin-left: 20px;
}

.title{
  font-family: 'Playfair Display', serif;
  color: #000;
  font-size: 55px;
  font-weight: 700;
}

.chartGenerator{
  width: fit-content;
  height: fit-content;
  z-index: 3;
  position: absolute;
  left: -10000px;
}

</style>
