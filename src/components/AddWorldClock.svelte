<script>
  import { createEventDispatcher } from "svelte";
  import Fa from "svelte-fa";
  import { faPlus } from "@fortawesome/free-solid-svg-icons";

  export let newTimeZone;

  const dispatch = createEventDispatcher();
</script>

<form on:submit|preventDefault={dispatch('submitTimeZone', newTimeZone)}>
  <input
    type="text"
    id="datetime-0"
    autocomplete="off"
    class="input input--lg"
    placeholder="Add timezones"
    bind:value={newTimeZone} />
  <button
    type="submit"
    disabled=""
    class="btn--lg btn--secondary"
    aria-pressed="false"
    aria-label="Add a timezone">
    <Fa icon={faPlus} id="fa-plus-icon" size="1.5x" color="--bg-main" />
  </button>
</form>
