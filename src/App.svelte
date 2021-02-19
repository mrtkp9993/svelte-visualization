<script>
  import {MaterialApp, AppBar, Col, Row} from 'svelte-materialify';
  import Table from "./components/Table.svelte";
  import Info from "./components/Info.svelte";
  import Error from "./components/Error.svelte";
  import Graph from "./components/Graph.svelte";

  let theme = 'light';

  async function getEarthquakeData() {
    const response = await fetch("https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&starttime=2014-01-01&minmagnitude=5");
    let data = await response.json();
    return data.features;
  }

  let promise = getEarthquakeData();

  var innerHeight;
</script>

<svelte:window bind:innerHeight={innerHeight} />

<MaterialApp {theme}>
  <AppBar>
    <span slot="title">USGS Earthquakes</span>
  </AppBar>
  <div class="container">
    <Row class="center" style="height: {innerHeight * 0.8}px">
    {#await promise}
      <Col><Info msg={'Data is loading...'}/></Col>
    {:then data}
      <Col><Table {data}/></Col>
      <Col><Graph {data}/></Col>
    {:catch error}
      <Col><Error msg={'Data cannot be loaded.'}/></Col>
    {/await}
    </Row>
  </div>
</MaterialApp>

<style>
  .container {
    padding: 8px;
    margin-bottom: 12px;
    background-color: var(--theme-app-bar);
  }
</style>