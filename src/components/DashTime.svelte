<script>
  import { onMount } from "svelte";
  import getHours from "date-fns/getHours";

  import CurrentTime from "./CurrentTime.svelte";
  import TimeSymbol from "./TimeSymbol.svelte";
  import WorldClockToggle from "./WorldClockToggle.svelte";
  import WorldClock from "./WorldClock.svelte";
  import AddWorldClock from "./AddWorldClock.svelte";

  let date = new Date();
  let hours = getHours(date);
  let timeZones = [];
  let newTimeZone = "";
  let newTimeZoneID;
  let clockOnly = false;

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

  function removeAllTimeZones() {
    timeZones.splice(0, timeZones.length);
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
        <TimeSymbol bind:hours />
        <WorldClockToggle bind:clockOnly />
      </div>
      <h1 id="current-time">
        <CurrentTime bind:date />
      </h1>
    </div>

    <hr />

    {#if !clockOnly}
      <AddWorldClock bind:newTimeZone on:submitTimeZone={addTimeZone} />

      <div class="btn-group remove-all">
        <button
          type="button"
          class="btn--danger"
          aria-pressed="false"
          on:click={removeAllTimeZones}>Remove all</button>
      </div>

      <WorldClock bind:date bind:timeZones />

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
