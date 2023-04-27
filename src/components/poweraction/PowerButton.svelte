<script>
  export let action;
  export let title;
</script>

<button class="power-button">
  <h2 class="power-title">{title}</h2>
</button>

<style lang=scss>
  .power-button {
    background-color: $darkest;
    border: none;
    padding: 0.4rem 2rem;
    width: 100%;
    transition: all 0.1s ease-in-out;

    &:hover {
      opacity: 60%;
    }
  }

  .power-title {
    font-size: 22px;
    font-weight: 500;
  }
</style>

