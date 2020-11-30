<script>
  import differenceInHours from "date-fns/differenceInHours";
  import { utcToZonedTime, format } from "date-fns-tz";
  import Fa from "svelte-fa";
  import { faTrash, faArrowsAlt } from "@fortawesome/free-solid-svg-icons";

  export let date;
  export let editButtonsVisible;
  let displayedTimeDiff;

  let timeZones = [
    { id: 1, timeZone: "America/Argentina/Buenos_Aires" },
    { id: 2, timeZone: "Europe/Oslo" },
    { id: 3, timeZone: "Australia/Sydney" },
  ];
  let totalTimeZones = timeZones.length;

  //const timeZone = "America/Argentina/Buenos_Aires";
  const pattern = "HH:mm:ss";
  // Get the last name of the full TZ name
  // and replace the underscore with a space
  $: formattedTimeZone = timeZone
    .split("/")
    .slice(-1)
    .pop()
    .replace(/_/g, " ");

  $: zonedDate = utcToZonedTime(date, timeZone);
  $: output = format(zonedDate, pattern, { timeZone: timeZone });

  $: timeDiff = differenceInHours(date, zonedDate);

  $: if (timeDiff > 0) {
    displayedTimeDiff = `${timeDiff} Hour(s) Behind`;
  } else if (timeDiff < 0) {
    // Math.abs() inverts the number to be positive
    // https://stackoverflow.com/a/4652112
    displayedTimeDiff = `${Math.abs(timeDiff)} Hour(s) Ahead`;
  } else {
    displayedTimeDiff = "No Time Difference";
  }
</script>

<ul role="list" class="datetime-list stack-large">
  <!-- datetime-1 -->
  <li class="datetime">
    <div class="cards">
      <div class="card">
        {#each timeZones as timeZone, index (timeZones.id)}
          <span class="time-elsewhere label-wrapper">
            <label for="datetime-1" class="datetime-label">
              <span>
                <span
                  class="location">{timeZone.timeZone}</span>
                <br />
                <span class="hours-behind">{displayedTimeDiff}</span>
              </span>
              <span class="world-time">{output}</span>
            </label>
          </span>
          {#if editButtonsVisible}
            <span class="btn-group">
              <!-- TODO?(alt): Make this one of those :: things infront of the label instead -->
              <button type="button" class="btn--secondary" aria-pressed="false">
                <Fa icon={faArrowsAlt} size="1.2x" />
                <!-- <span class="visually-hidden">Jakarta</span> -->
              </button>
              <button type="button" class="btn--danger" aria-pressed="false">
                <Fa icon={faTrash} size="1.2x" />
                <!-- <span class="visually-hidden">Jakarta</span> -->
              </button>
            </span>
          {/if}
        {/each}
      </div>
    </div>
  </li>
</ul>
