<script>
  import differenceInHours from "date-fns/differenceInHours";
  import { utcToZonedTime, format } from "date-fns-tz";

  export let date;
  export let timeZone;
  let displayedTimeDiff;

  const pattern = "HH:mm";
  // Get the last name of the full TZ name
  // and replace the underscore with a space
  let formattedTimeZone = timeZone
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

<span class="time-elsewhere label-wrapper">
  <label for="datetime-1" class="datetime-label">
    <span>
      <span class="location">{formattedTimeZone}</span>
      <br />
      <span class="hours-behind">{displayedTimeDiff}</span>
    </span>
    <span class="world-time">{output}</span>
  </label>
</span>
