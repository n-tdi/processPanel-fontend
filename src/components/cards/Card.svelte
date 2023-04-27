<script>
  export let title;
</script>

<div class="card-container">
  <h3 class="card-title">{title}</h3>
  <div class="slot-container">
    <slot></slot>
  </div>
</div>

<style lang=scss>
  .card-container {
    height: 300px;
    filter: drop-shadow(0 0 5px #00000098);
    padding: 1.2rem;
    padding-left: 1.5rem;
    border-radius: 10px;
    margin-bottom: 2rem;
    background-color: $darkest;
  }

  .card-title {
    font-size: 22px;
    font-weight: 600;
  }
</style>