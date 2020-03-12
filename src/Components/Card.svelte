<script>
  export let title = "";
  export let description = "";
  export let background = "#FFFFFF";
  export let color = "#000000";
</script>

<main style="background-color: {background}; color: {color}">
  <div class="content">
    <div class="info">
      {#if title}
        <p class="title">{title}</p>
      {/if}
      {#if description}
        <p class="description">{description}</p>
      {/if}
    </div>
    <slot>
      <p align="center">Ops! Sembra non esserci niente</p>
    </slot>
  </div>
</main>

<style>
  main{
    width: 100%;
    min-height: 100%;
    height: fit-content;

    border: 5px solid #c5cae9;
    border-radius: 5px;
  }

  .content{
    position: relative;
    display: block;
    margin: 25px;
    height: 100%;
  }

  .info{
    line-height: 6px;
  }

  .info .title{
    font-weight: 800;
    color: #000;
    font-size: 20px;
    font-family: 'Playfair Display', serif;
    font-weight: 400;
  }

  .info .description{
    line-height: 18px;
  }
</style>
