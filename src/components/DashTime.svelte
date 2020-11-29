<script>
  import getHours from "date-fns/getHours";

  import CurrentTime from "./CurrentTime.svelte";
  import TimeSymbol from "./TimeSymbol.svelte";
  import WorldClockToggle from "./WorldClockToggle.svelte";

  import Fa from "svelte-fa";
  import {
    faPlus,
    faTrash,
    faArrowsAlt,
  } from "@fortawesome/free-solid-svg-icons";

  let clockOnly = false;
  let manualDarkMode = false;
  let date = new Date();
  let hours = getHours(date);

  let editButtonsVisible = false;
  const toggleEditButtonsVisibility = () => {
    editButtonsVisible = !editButtonsVisible;
  };
</script>

<div class="dashtime-app">
  <div style="max-width: 640px">
    <!-- CurrentClientTime -->
    <div id="client-current-time">
      <div class="header">
        <TimeSymbol bind:manualDarkMode bind:hours />
        <WorldClockToggle bind:clockOnly />
      </div>
      <h1 id="current-time">
        <CurrentTime bind:date/>
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
                  <span class="world-time">12:37:00</span>
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
