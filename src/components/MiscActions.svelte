<script>
  export let editButtonsVisible;
  export let timeZones;

  const toggleEditButtonsVisibility = () => {
    editButtonsVisible = !editButtonsVisible;
  };

  const removeAllTimeZones = () => {
    timeZones.splice(0, timeZones.length);
  };
</script>

<div class="btn-group misc-actions">
  <button
    type="button"
    class="btn--primary"
    aria-pressed="false"
    on:click={toggleEditButtonsVisibility}>Toggle edit mode</button>
  <button
    type="button"
    class="btn--danger"
    aria-pressed="false"
    on:click={removeAllTimeZones}>Remove all</button>
</div>
