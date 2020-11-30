<script>
  import { onMount } from "svelte";
  import getHours from "date-fns/getHours";

  import CurrentTime from "./CurrentTime.svelte";
  import TimeSymbol from "./TimeSymbol.svelte";
  import WorldClockToggle from "./WorldClockToggle.svelte";
  import WorldClock from "./WorldClock.svelte";

  import Fa from "svelte-fa";
  import { faPlus } from "@fortawesome/free-solid-svg-icons";

  let clockOnly = false;
  let manualDarkMode = false;
  let date = new Date();
  let hours = getHours(date);

  let editButtonsVisible = false;
  const toggleEditButtonsVisibility = () => {
    editButtonsVisible = !editButtonsVisible;
  };

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
      <!-- AddWorldClock -->
      <form>
        <input
          type="text"
          id="datetime-0"
          autocomplete="off"
          class="input input--lg"
          placeholder="Add timezones" />
        <button
          type="submit"
          disabled=""
          class="btn--lg btn--secondary"
          aria-pressed="false"
          aria-label="Add a timezone">
          <Fa icon={faPlus} id="fa-plus-icon" size="1.5x" color="--bg-main" />
        </button>
      </form>

      <!-- MiscActions -->
      <div class="btn-group misc-actions">
        <button
          type="button"
          class="btn--primary"
          aria-pressed="false"
          on:click={toggleEditButtonsVisibility}>Toggle edit mode</button>
        <button type="button" class="btn--danger" aria-pressed="false">Remove
          all</button>
      </div>

      <!-- WorldClockList -->
      <WorldClock bind:date bind:editButtonsVisible />
      <hr style="margin-bottom: 0.5rem; margin-top: 2rem;" />
    {/if}
    <footer>
      <div class="footer-text">
        Colour palette is based on the
        <a href="https://horizontheme.netlify.app/">Horizon theme</a>.
      </div>
      <div class="footer-text">
        By
        <a href="iamrifki.github.io">Dania Rifki</a>.
      </div>
    </footer>
  </div>
</div>
