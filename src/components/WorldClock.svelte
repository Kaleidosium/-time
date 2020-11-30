<script>
  import TimeCard from "./TimeCard.svelte";
  export let date;
  export let editButtonsVisible;

  let timeZones = [
    { id: 1, timeZone: "America/Argentina/Buenos_Aires" },
    { id: 2, timeZone: "Europe/Oslo" },
    { id: 3, timeZone: "Australia/Sydney" },
  ];
</script>

<ul role="list" class="datetime-list stack-large">
  <!-- datetime-1 -->
  <li class="datetime">
    <div class="cards">
      {#each timeZones as _timeZones, index (_timeZones.id)}
        <TimeCard bind:date bind:editButtonsVisible bind:timeZone={_timeZones.timeZone} />
      {/each}
    </div>
  </li>
</ul>
