<svelte:head>
  <title>Chart Generator</title>
  <meta name="description" content="A chart generator" />
  <meta name="keywords" content="graph, generator, opensource, svelte" />
  <meta name="author" content="Massimo Moffa" />
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&display=swap" rel="stylesheet">
</svelte:head>

<script>
	import {onMount} from 'svelte';
  import { title_stored, label_stored, data_stored } from './stored_data.js';
	import Header from './Components/Header.svelte';
	import Card from './Components/Card.svelte';
	import Graph from './Components/Graph.svelte';
	import Grid from 'svelte-grid';
	import gridHelp from "svelte-grid/build/helper/index.mjs";
  import Configuration from './Widget/Configuration.svelte';
  import Dataset from './Widget/Dataset.svelte';
  import Label from './Widget/Label.svelte';
  import Exporter from './Widget/Exporter.svelte';

	let items_arr = [
		gridHelp.item({ x: 0, y: 0, w: 3, h: 4, id: "preview_container", title: null, description: null, resizable: false}),
    gridHelp.item({ x: 2, y: 0, w: 2, h: 4, id: "configuration_container", title: "Configurazione", description: null, resizable: false}),
    gridHelp.item({ x: 0, y: 4, w: 5, h: 2, id: "labels_container", title: "Labels", description: null, resizable: false}),
    gridHelp.item({ x: 0, y: 6, w: 5, h: 3, id: "dataset_container", title: "Dataset", description: null, resizable: false}),
	];
  let breakpoints = [
    [1000, 1, 3],
  ]

	onMount(() => {
		//Prima di tutto il grafico
		const graph = new Graph({
			target: document.querySelector("#preview_container"),
			props: {}
		});

    //Ora tocca al widget per i label
    const label = new Label({
			target: document.querySelector("#labels_container"),
			props: {},
		});

    //Poi il widget per la configurazione
    const configuration = new Configuration({
			target: document.querySelector("#configuration_container"),
			props: {},
		}).$on("exportChart", (ris) => {
      let exportChart = new Exporter({
        target: document.body,
        props: ris.detail,
      });
      exportChart.$set({
        ctx: exportChart,
      });
    });

    //Ed infine il widget per gestire i dataset
    const dataset = new Dataset({
      target: document.querySelector("#dataset_container"),
      props: {},
    });
	});
</script>

<main>
	<Header />
	<Grid useTransform {breakpoints} items={items_arr} bind:items_arr cols={5} let:item rowHeight={90} gap={20}>
  	<Card title={item.title} description={item.description}>
  		<div class="content_container" id={item.id}>
        {#if item.content}
          {@html item.content}
        {/if}
      </div>
  	</Card>
	</Grid>
</main>

<style>

  ::-webkit-scrollbar {
    width: 7px;
  }

  ::-webkit-scrollbar-track {
    background: #fff;
  }

  ::-webkit-scrollbar-thumb {
    background: #5c6bc0;
  }

  ::-webkit-scrollbar-thumb:hover {
    background: #4454b1;
  }

	:global(body){
		overflow: hidden !important;
	}

	:global(.svlt-grid-container) {
    margin: 0 30px;
  }

	main {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		left: 0;

		background-color: #fff;
		overflow-y: auto;
    scrollbar-color: #5c6bc0 #fff;
    scrollbar-width: thin;

    background: url('../media/image/background-page.svg') no-repeat;
    background-size: cover;
	}

  .content_container{
    height: 90%;
  }

</style>
