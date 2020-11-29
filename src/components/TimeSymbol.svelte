<script>
  import Fa from "svelte-fa";
  import { faSun, faMoon } from "@fortawesome/free-solid-svg-icons";

  // TODO(alt): Store manualDarkMode to LocalStorage
  // https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API
  export let hours;
  export let manualDarkMode;

  const toggleTheme = () => {
    manualDarkMode = !manualDarkMode;
  };

  $: if (hours >= 18 || hours <= 6 || manualDarkMode) {
    document.body.classList.toggle("dark-mode");
  }
</script>

<span id="time-symbol" title="Toggle Light/Dark Mode" on:click={toggleTheme}>
  {#if hours >= 18 || hours <= 6}
    <Fa icon={faMoon} id="fa-moon-icon" size="2x" color="#FDF0ED" />
  {:else}
    <Fa icon={faSun} id="fa-sun-icon" size="2x" color="#FDF0ED" />
  {/if}
</span>
