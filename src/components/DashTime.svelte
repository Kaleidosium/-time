<script>
  import getHours from "date-fns/getHours";

  import CurrentTime from "./CurrentTime.svelte";
  import TimeSymbol from "./TimeSymbol.svelte";

  import Fa from "svelte-fa";
  import {
    faPlus,
    faTrash,
    faArrowsAlt,
    faEye,
    faEyeSlash,
  } from "@fortawesome/free-solid-svg-icons";

  let clockOnly = false;
  let manualDarkMode = false;
  let date = new Date();
  let hours = getHours(date);

  const toggleTheme = () => {
    manualDarkMode = !manualDarkMode;
  };

  const toggleWorldClock = () => {
    clockOnly = !clockOnly;
  };

  let editButtonsVisible = false;
  const toggleEditButtonsVisibility = () => {
    editButtonsVisible = !editButtonsVisible;
  };

  $: if (hours >= 18 || hours <= 6 || manualDarkMode) {
    document.body.classList.toggle("dark-mode");
  }
</script>

<div class="dashtime-app">
  <div style="max-width: 640px">
    <!-- CurrentClientTime -->
    <div id="client-current-time">
      <div class="header">
        <span
          id="time-symbol"
          title="Toggle Light/Dark Mode"
          on:click={toggleTheme}>
          <TimeSymbol />
        </span>
        <span class="world-clock-toggle" on:click={toggleWorldClock}>
          {#if !clockOnly}
            <Fa icon={faEyeSlash} id="fa-plus-icon" color="--text" />
            Hide World Clock
          {:else}
            <Fa icon={faEye} id="fa-plus-icon" color="--text" />
            View World Clock
          {/if}
        </span>
      </div>
      <h1 id="current-time">
        <CurrentTime />
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
          class="input input__lg"
          placeholder="Add timezones" />
        <button
          type="submit"
          disabled=""
          class="btn btn__lg"
          aria-pressed="false">
          <!-- TODO(alt): Use fa-plus for symbol to be more consistent -->
          <Fa icon={faPlus} id="fa-plus-icon" size="1.5x" color="--bg-main" />
        </button>
      </form>

      <!-- MiscActions -->
      <div class="btn-group misc-actions">
        <button
          type="button"
          class="btn btn__primary"
          aria-pressed="false"
          on:click={toggleEditButtonsVisibility}>Toggle edit mode</button>
        <button
          type="button"
          class="btn btn__danger"
          aria-pressed="false">Remove all</button>
      </div>

      <!-- WorldClockList -->
      <ul
        role="list"
        class="datetime-list stack-large"
        aria-labelledby="list-heading">
        <!-- datetime-1 -->
        <li class="datetime">
          <div class="cards">
            <div class="card">
              <span class="time-elsewhere label-wrapper">
                <label for="datetime-1" class="datetime-label">
                  <span>
                    <span class="location">Berlin</span>
                    <br />
                    <span class="hours-behind">6 Hours Behind</span>
                  </span>
                  <span class="time">12:37:00</span>
                </label>
              </span>
              {#if editButtonsVisible}
                <!-- TODO(alt): Make these only visible when enabling edit mode -->
                <span class="btn-group">
                  <!-- TODO(alt): Make this one of those :: things infront of the label instead -->
                  <button
                    type="button"
                    class="btn btn__secondary"
                    aria-pressed="false">
                    <Fa icon={faArrowsAlt} size="1.2x" />
                    <!-- <span class="visually-hidden">Jakarta</span> -->
                  </button>
                  <button
                    type="button"
                    class="btn btn__danger"
                    aria-pressed="false">
                    <Fa icon={faTrash} size="1.2x" />
                    <!-- <span class="visually-hidden">Jakarta</span> -->
                  </button>
                </span>
              {/if}
            </div>
          </div>
        </li>
      </ul>
    {/if}
  </div>
</div>
