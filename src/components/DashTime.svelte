<script>
  import { onMount } from "svelte";
  import getHours from "date-fns/getHours";

  import CurrentTime from "./CurrentTime.svelte";
  import TimeSymbol from "./TimeSymbol.svelte";
  import WorldClockToggle from "./WorldClockToggle.svelte";
  import WorldClock from "./WorldClock.svelte";
  import MiscActions from "./MiscActions.svelte";
  import AddWorldClock from "./AddWorldClock.svelte"

  let clockOnly = false;
  let manualDarkMode = false;
  let date = new Date();
  let hours = getHours(date);
  let editButtonsVisible = false;
  let timeZones = [];
  let newTimeZone = "";
  let newTimeZoneID;

  $: totalTimeZones = timeZones.length;
  $: {
    if (totalTimeZones === 0) {
      newTimeZoneID = 1;
    } else {
      newTimeZoneID = Math.max(...timeZones.map(t => t.id)) + 1;
    }
  }

  function addTimeZone() {
    timeZones = [...timeZones, { id: newTimeZoneID, timeZone: newTimeZone }];
    newTimeZone = "";
  }

  onMount(() => {
    const interval = setInterval(() => {
      date = new Date();
    }, 1000);
  });
</script>

<div class="dashtime-app">
  <div class="container">
    <!-- CurrentClientTime -->
    <div id="client-current-time">
      <div class="header">
        <TimeSymbol bind:manualDarkMode bind:hours />
        <WorldClockToggle bind:clockOnly />
      </div>
      <h1 id="current-time">
        <CurrentTime bind:date />
      </h1>
    </div>

    <hr />

    {#if !clockOnly}
      <AddWorldClock bind:newTimeZone on:submitTimeZone={addTimeZone} />
       
      <MiscActions bind:editButtonsVisible bind:timeZones />

      <WorldClock bind:date bind:editButtonsVisible bind:timeZones />

      <hr style="margin-bottom: 0.5rem; margin-top: 2rem;" />
    {/if}
    <footer>
      <div class="footer-text">
        Colour palette is based on the
        <a href="https://horizontheme.netlify.app/">Horizon theme</a>
      </div>
      <div class="footer-text">
        By
        <a href="iamrifki.github.io">Dania Rifki</a>
      </div>
    </footer>
  </div>
</div>
