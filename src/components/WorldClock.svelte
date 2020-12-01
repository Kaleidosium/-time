<script>
  import Fa from "svelte-fa";
  import { faTrash, faArrowsAlt } from "@fortawesome/free-solid-svg-icons";

  import TimeCard from "./TimeCard.svelte";
  
  export let date;
  export let editButtonsVisible;
  export let timeZones;

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
              <span class="visually-hidden">Move {timeZone.timeZone}</span>
            </button>
            <button type="button" class="btn--danger" on:click={() => removeTimeZone(timeZone)} aria-pressed="false">
              <Fa icon={faTrash} size="1.2x" />
              <span class="visually-hidden">Delete {timeZone.timeZone}</span>
            </button>
          </span>
        {/if}
        </div>
      {/each}
    </div>
  </li>
</ul>
