<script>
  // import Header from './Header.svelte';
  import "./styles.css";
  import { onMount } from "svelte";
  // Create a store to hold the JSON data
  import { writable } from "svelte/store";
  import { derived } from "svelte/store";

  const jsonData = writable(null);
  // Define the path to your JSON file
  const jsonFilePath = "../data/csvjson.json";
  let data, graphics, writing, maplab
  // Function to load and parse the JSON data
  async function loadJsonData() {
    try {
      const response = await fetch(jsonFilePath);
      const data = await response.json();
      jsonData.set(data);
    } catch (error) {
      console.error("Error loading JSON data:", error);
    }
  }

  // Use the onMount lifecycle function to load the JSON data when the page is mounted
  $: onMount(loadJsonData);

  function filterDataByClass(classValue) {
    if ($jsonData) {
      return $jsonData.filter((entry) => entry.class === classValue);
    }
    return [];
  }

  $: if ($jsonData) {
    data = filterDataByClass("data");
    graphics = filterDataByClass("graphics");
    writing = filterDataByClass("writing");
    maplab = filterDataByClass("maplab");
  }
  // now filter the json to get multiple categories
</script>

<div>
  <h1>Marie Patino</h1>
  <p>
    I'm a graphics journalist based in Brooklyn, New York, currently working at
    Bloomberg News. I maintained the Bloomberg CityLab <a href='https://www.bloomberg.com/citylab/maplab'>MapLab</a> newsletter for a bit, that's a newsletter about maps.
  </p>
  <p>Here's a selection of some of the things I've worked on</p>
</div>
<div class="list-work">
  <p class='header'>Graphics</p>
  {#if $jsonData}
    {#each graphics as graphic}
      <li><span class='date'>{graphic.date}</span> - <a href={graphic.url}>{graphic.title}</a></li>
    {/each}
  {/if}

  <p class='header'>Data crunching</p>
  {#if $jsonData}
    {#each data as d}
      <li><span class='date'>{d.date}</span> - <a href={d.url}>{d.title}</a></li>
    {/each}
  {/if}
  
  <p class='header'>Some writing about maps</p>
  {#if $jsonData}
    {#each maplab as map}
      <li><span class='date'>{map.date}</span> - <a href={map.url}>{map.title}</a></li>
    {/each}
  {/if}
  
  <p class='header'>Some misc writing</p>
  {#if $jsonData}
    {#each writing as w}
      <li><span class='date'>{w.date}</span> - <a href={w.url}>{w.title}</a></li>
    {/each}
  {/if}
</div>

<style>
  h1,
  p,
  h3,
  li {
    font-family: Quantico;
    color:black
  }
  a{
    color:black;
  }
  .date{
    font-size:13px;
  }
  .header{
    font-size:1.1em;
  }
</style>
