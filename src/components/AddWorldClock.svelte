<script>
  import { createEventDispatcher } from "svelte";
  import timeZoneJSONData from "tzdata";
  import Fa from "svelte-fa";
  import { faPlus } from "@fortawesome/free-solid-svg-icons";

  export let newTimeZone;

  const dispatch = createEventDispatcher();
  const timeZoneData = Object.keys(timeZoneJSONData.zones);
</script>

<form on:submit|preventDefault={dispatch('submitTimeZone', newTimeZone)}>
  <input
    type="text"
    id="datetime-input"
    list="timeZoneList"
    class="input input--lg"
    placeholder="Add timezones"
    autocomplete="off"
    bind:value={newTimeZone} 
    required
    />
  <label for="datetime-input" aria-label="Add timezones" />
  <datalist id="timeZoneList">
    {#each timeZoneData as listedTimeZone}
      <option value={listedTimeZone} />
    {/each}
  </datalist>
  <button
    type="submit"
    disabled=""
    class="btn--lg btn--secondary"
    aria-pressed="false"
    aria-label="Add a timezone">
    <Fa icon={faPlus} id="fa-plus-icon" size="1.5x" color="--bg-main" />
  </button>
</form>
