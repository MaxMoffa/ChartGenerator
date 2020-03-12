<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  export let text = "Button";
  export let backgroundColor = "#303f9f";
  export let disabled = false;

  function click() {
    if(!disabled) dispatch("click", {});
  }
</script>

<div class={disabled ? "disabled" : ""} style="background-color: {backgroundColor};" on:click={click}>{text}</div>

<style>
  div:hover{
    background-color: #1a237e !important;
    transition: 0.3s background;
  }
  div{
    margin: 6px 0;
    cursor: pointer;
    border-radius: 6px;
    color: #fff;
    padding: 10px 18px;
    font-family: 'Playfair Display', serif;
    font-weight: 700;
    text-align: center;
    user-select: none;
    transition: 0.3s background;
  }
  .disabled{
    background-color: #455a64 !important;
    cursor: not-allowed;
  }
  .disabled:hover{
    background-color: #455a64 !important;
  }
</style>
