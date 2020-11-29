<script>
  import format from "date-fns/format";

  export let date;

  $: day = format(date, "cccc, ");
  $: dateDate = format(date, "MMMM do, u,");
  $: time = format(date, "HH:mm:ss");
</script>

<div class="local-time">
  <div id="day">{day}</div>
  <div id="date">{dateDate}</div>
  <div id="time">{time}</div>
</div>
