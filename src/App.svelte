<script>
  import { onMount } from 'svelte';
  let first;
  let last;

  $: show = first !== undefined && last !== undefined && first !== null && last !== null && first !== last;
  $: sign = first < last ? '+' : '-';
  $: color = first < last ? '#0ff008' : '#ff3e00';
  $: change = Math.abs((last-first)/first*100).toFixed(2)+"%";

  onMount(() => {
    document.getElementById("first").focus();
  });
</script>

<main>
  {#if show}
    <h1 style="color: {color}">{ sign } { change }</h1>
  {:else}
    <h1 class="title">Enter two different values</h1>
  {/if}

  <input id="first" type="number" step="any" placeholder="First value" bind:value={first}>
  <input id="last" type="number" step="any" placeholder="Last value" bind:value={last}>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;

    background-color: #202124;
  }

  main {
    text-align: center;
    padding: 1em;
    margin-top: 35vh;
  }

  h1 {
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 300;
    line-height: 1.1;
    margin: 2rem auto;
  }

  h1.title {
    color: #e8eaed;
  }

  input {
    height: 40px;
    width: 30vw;
    border-radius: 15px;
    border: 1px solid rgba(223,225,229,0);
    background-color: #303134;
    color: #e8eaed;
    font-size: large;
    padding-left: 13px;
    margin-bottom: 15px;
  }
  
  input:focus{
    outline: none;
  }

  input[type='number'] {
    -moz-appearance:textfield;
  }

  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
  }

@media only screen 
  and (min-width: 320px) 
  and (max-width: 950px) {
    h1 {
      font-size: 1.2rem;
      font-weight: 300;
    }

    input {
      width: 80vw;
    } 

    main {
      margin-top: 30vh;
    }
  }
</style>
