<script>
  import Fa from "svelte-fa";

  import { faEye, faEyeSlash } from "@fortawesome/free-solid-svg-icons";

  export let clockOnly = false;

  const toggleWorldClock = () => {
    clockOnly = !clockOnly;
  };
</script>

<span class="world-clock-toggle" on:click={toggleWorldClock}>
  {#if !clockOnly}
    <Fa icon={faEyeSlash} id="fa-plus-icon" color="--text" />
    Hide World Clock
  {:else}
    <Fa icon={faEye} id="fa-plus-icon" color="--text" />
    View World Clock
  {/if}
</span>
