<script>
  import format from "date-fns/format";

  function tick() {
    document.getElementById("day").innerHTML = format(new Date(), "cccc, ");
    document.getElementById("date").innerHTML = format(
      new Date(),
      "MMMM do, u,",
    );
    document.getElementById("time").innerHTML = format(new Date(), "kk:mm:ss");
  }

  window.onload = tick;
  window.setInterval(tick, 60);
</script>

<div class="local-time">
  <div id="day" />
  <div id="date" />
  <div id="time" />
</div>
