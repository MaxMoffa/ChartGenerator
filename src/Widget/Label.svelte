<script>
  import { title_stored, label_stored, data_stored } from '../stored_data.js';

  export let labels = []

  label_stored.subscribe(value => {
		labels = value;
	});

  function handleChange(data) {
    labels[parseInt(data.target.id)] = data.target.value;
    label_stored.set(labels);
  }
</script>

<main>
  {#if labels.length > 0}
    <div class="labels_container">
      {#each labels as label, i}
        <input type="text" id="{i}" name="title" placeholder={"Label #" + i} on:change={handleChange} bind:value={labels[i]}>
      {/each}
    </div>
  {:else}
    Ancora nulla...
  {/if}
</main>

<style>
  main{
    overflow-y: hidden;
    overflow-x: auto;
  }

  main *{
    margin-right: 2px;
  }

  .labels_container{
    overflow-x: auto;
    overflow-y: hidden;
    white-space: nowrap;

    scrollbar-color: #5c6bc0 #fff;
    scrollbar-width: thin;
  }

  .labels_container *{
    display: inline-block;
  }

  .labels_container::-webkit-scrollbar {
    width: 7px;
  }

  .labels_container::-webkit-scrollbar-track {
    background: #fff;
  }

  .labels_container::-webkit-scrollbar-thumb {
    background: #5c6bc0;
  }

  .labels_container::-webkit-scrollbar-thumb:hover {
    background: #4454b1;
  }
</style>
