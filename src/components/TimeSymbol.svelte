<script>
  import getHours from "date-fns/getHours";

  import Fa from "svelte-fa";
  import { faSun, faMoon } from "@fortawesome/free-solid-svg-icons";

  const hours = getHours(new Date());
</script>

{#if hours >= 18 || hours <= 6}
  <Fa icon={faMoon} id="fa-moon-icon" size="2x" color="#FDF0ED" />
{:else}
  <Fa icon={faSun} id="fa-sun-icon" size="2x" color="#FDF0ED" />
{/if}
