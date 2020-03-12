<script>
  import { title_stored, label_stored, data_stored } from '../stored_data.js';
  import { createEventDispatcher } from 'svelte';
  import Button from "../Components/Button.svelte";

  const dispatch = createEventDispatcher();
  const fileReader = new FileReader();

  let title = null;
  let isData = true;
  let data = {
    title: "",
    label: [],
    data: []
  }

  title_stored.subscribe(value => {
    data.title = value;
  });

  label_stored.subscribe(value => {
    data.label = value;
  });

  data_stored.subscribe(value => {
    data.data = value;
  });

  fileReader.onload = (data) => {
    let res = CsvToMatrix(data.target.result)
    label_stored.set(res.labels);
    isData = false;
    data_stored.set(res.data);
  };

  function handleChange() {
    title_stored.set(title);
  }

  function loadFile() {
    console.log("Open a file");
    document.getElementById('file-input').click();
    document.getElementById('file-input').onchange = function(e) {
      let file = e.target.files[0];
      fileReader.readAsText(file);
    };
  }

  function CsvToMatrix(data) {
    let dataset = 0;
    let result = {
      data: [],
      labels: []
    }
    data = data.split("\r\n");
    data.forEach((item, i) => {
      let row = [];
      if (i>0) {
        item.split(";").forEach((item, i) => {
          if(!isNaN(parseFloat(item))) row.push(parseFloat(item));
        });
      }else {
        item.split(";").forEach((item, i) => {
          if(item !== "") result.labels.push(item);
        });
      }
      if(row.length !== 0) result.data.push({
        label: "Label #" + (dataset++),
        type: "line",
        backgroundColor: "",
        borderColor: "#000",
        data: row,
        borderDash: []
      });
    });
    return result;
  }

  function exportChart() {
    dispatch("exportChart", data)
  }
</script>

<input type="text" id="title" name="title" placeholder="Titolo" on:change={handleChange} bind:value={title}>
<Button text="Carica un CSV" on:click={loadFile}/>
<Button text="Esporta il grafico" disabled={isData} on:click={exportChart} backgroundColor="#512da8"/>
<input id="file-input" type="file" accept=".csv" name="name" style="display: none;" />
<p align="justify">*Il CSV deve essere strutturato usando una riga per ogni dato, in particolare la prima riga deve contenere gli elementi da visualizzare sull'asse delle ascisse</p>
