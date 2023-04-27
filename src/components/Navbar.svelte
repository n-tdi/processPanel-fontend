<script>
  import PowerButton from "./poweraction/PowerButton.svelte";

  export let title;
</script>

<header class="nav-bar">
  <div class="flex-container">
    <div class="split">
      <h1 class="nav-title">{title}</h1>
      <p class="nav-description">Ntdi World</p>
    </div>
    <div class="split-btn">
      <PowerButton title="Start" action="start" />
      <div class="bars">
        <PowerButton action="stop" title="Stop" />
      </div>
      <div class="bars">
        <PowerButton action="restart" title="Restart" />
      </div>
    </div>
  </div>
</header>

<style lang=scss>
  header {
    background-color: $darkest;
    padding: 2rem 0;
    filter: drop-shadow(0 0 5px #00000098);
  }

  .flex-container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    max-width: $max-width;
    margin: 0 auto;
  }
  
  .nav-title {
    margin-bottom: 4px;
  }

  .nav-description {
    opacity: 50%;
    font-size: 16px;
  }

  .split-btn {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .bars {
    border-left: 2px solid $dark;
  }
</style>