<script>
  import TimeCard from "./TimeCard.svelte";
  
  export let date;
  export let timeZones;
</script>

<ul role="list" class="datetime-list stack-large">
  <li class="datetime">
    <div class="cards">
      {#each timeZones as timeZone, index (timeZone.id)}
          <TimeCard bind:date bind:timeZone={timeZone.timeZone} />
      {/each}
    </div>
  </li>
</ul>
