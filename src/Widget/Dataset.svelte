<script>
  import { data_stored } from '../stored_data.js';

  let id = 0;
  export let data = [];

  data_stored.subscribe(value => {
    data = value;
  });

  function handleChange(info) {
    console.log(info);
    if(info.target.placeholder === "Trattegiata"){
      if(info.target.checked) data[id].borderDash = [10];
      else data[id].borderDash = [];
    }
    data_stored.set(data);
  }

</script>

<main>
  {#if data.length > 0}
    <select bind:value={id}>
      {#each data as element, i}
        <option value={i}>Dataset #{i}</option>
      {/each}
    </select>
    <div>
      <label for="{id}_label">Nome</label>
      <input type="text" id="{id}_label" placeholder="Nome" on:change={handleChange} bind:value={data[id].label}>
    </div>
    <label for="{id}_type">Tipo di grafico</label>
    <select id="{id}_type" on:change={handleChange} bind:value={data[id].type}>
      <option value="line">Linea</option>
      <option value="bar">Barre</option>
    </select>
    <div>
      <label for="{id}_background">Colore dello sfondo</label>
      <input type="color" id="{id}_background" placeholder="Sfondo" on:change={handleChange} bind:value={data[id].backgroundColor}>
    </div>
    <div>
      <label for="{id}_border">Colore dello bordo</label>
      <input type="color" id="{id}_border" placeholder="Bordo" on:change={handleChange} bind:value={data[id].borderColor}>
    </div>
    <div>
      <label for="{id}_dash">Linea trattegiata</label>
      <input type="checkbox" id="{id}_dash" placeholder="Trattegiata" on:change={handleChange} checked={!(data[id].borderDash.length === 0)}>
    </div>
    <label for="{id}_data_container">Valori</label>
    <div id="{id}_data_container" class="data_container">
      {#each data[id].data as element, i}
        <input type="text" id="{id}:{i}" placeholder={"Data #" + i} on:change={handleChange} bind:value={element}>
      {/each}
    </div>
  {:else}
    Ancora nulla...
  {/if}
</main>

<style>
  .data_container{
    overflow-x: auto;
    overflow-y: hidden;
    white-space: nowrap;

    scrollbar-color: #5c6bc0 #fff;
    scrollbar-width: thin;
  }

  .data_container::-webkit-scrollbar {
    width: 7px;
  }

  .data_container::-webkit-scrollbar-track {
    background: #fff;
  }

  .data_container::-webkit-scrollbar-thumb {
    background: #5c6bc0;
  }

  .data_container::-webkit-scrollbar-thumb:hover {
    background: #4454b1;
  }

  .data_container *{
    display: inline-block;
    margin-left: 2px;
  }

  main *{
    margin: 8px 0;
  }
</style>
