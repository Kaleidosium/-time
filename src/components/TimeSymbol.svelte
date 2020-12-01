<script>
  import Fa from "svelte-fa";
  import { faSun, faMoon } from "@fortawesome/free-solid-svg-icons";
  
  export let hours;
  export let manualDarkMode;

  const toggleTheme = () => {
    manualDarkMode = !manualDarkMode;
  };

  $: if (hours > 17 || hours < 6 || manualDarkMode) {
    document.body.classList.toggle("dark-mode");
  }
</script>

<button id="time-symbol" title="Toggle Light/Dark Mode" on:click={toggleTheme} aria-pressed="false">
  {#if hours > 17 || hours < 6}
    <Fa icon={faMoon} id="fa-moon-icon" size="2x" color="#FDF0ED" />
  {:else}
    <Fa icon={faSun} id="fa-sun-icon" size="2x" color="#FDF0ED" />
  {/if}
</button>
