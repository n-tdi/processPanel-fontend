<script>
  import PowerButton from "./PowerButton.svelte";
</script>

<div class="button-wrapper">
  <PowerButton action="start" title="Start"/>
  <PowerButton action="stop" title="Stop" />
  <PowerButton action="restart" title="Restart" />
</div>

<style lang=scss>
  .button-wrapper {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: start;
  }
</style>