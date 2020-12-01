<script>
  import Fa from "svelte-fa";
  import { faTrash, faArrowsAlt } from "@fortawesome/free-solid-svg-icons";

  import TimeCard from "./TimeCard.svelte";
  export let date;
  export let editButtonsVisible;

  let timeZones = [
    { id: 1, timeZone: "America/Argentina/Buenos_Aires" },
    { id: 2, timeZone: "Europe/Oslo" },
    { id: 3, timeZone: "Australia/Sydney" },
  ];

  function removeTimeZone(timeZone) {
    timeZones = timeZones.filter(tz => tz.id !== timeZone.id);
  }
</script>

<ul role="list" class="datetime-list stack-large">
  <!-- datetime-1 -->
  <li class="datetime">
    <div class="cards">
      {#each timeZones as timeZone, index (timeZone.id)}
        <div class="card">
          <TimeCard bind:date bind:timeZone={timeZone.timeZone} />
          {#if editButtonsVisible}
          <span class="btn-group card-btn-group">
            <!-- TODO?(alt): Make this one of those :: things infront of the label instead -->
            <button type="button" class="btn--secondary" aria-pressed="false">
              <Fa icon={faArrowsAlt} size="1.2x" />
              <!-- <span class="visually-hidden">Jakarta</span> -->
            </button>
            <button type="button" class="btn--danger" on:click={() => removeTimeZone(timeZone)} aria-pressed="false">
              <Fa icon={faTrash} size="1.2x" />
              <!-- <span class="visually-hidden">Jakarta</span> -->
            </button>
          </span>
        {/if}
        </div>
      {/each}
    </div>
  </li>
</ul>
