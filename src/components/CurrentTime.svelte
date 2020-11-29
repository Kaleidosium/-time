<script>
  import format from "date-fns/format";

  export let date;

  function tick() {
    document.getElementById("day").innerHTML = format(date, "cccc, ");
    document.getElementById("date").innerHTML = format(
      date,
      "MMMM do, u,",
    );
    document.getElementById("time").innerHTML = format(date, "kk:mm:ss");
  }

  window.onload = tick;
  window.setInterval(tick, 60);
</script>

<div class="local-time">
  <div id="day" />
  <div id="date" />
  <div id="time" />
</div>
