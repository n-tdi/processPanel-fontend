<script>
  export let submitFunction;

  let key = '';
</script>

<div class="container">
  <form class="auth-form">
    <div class="background">
      <h3 class="auth-title">Sign In</h3>
      <input type="text" class="auth-input" bind:value={key} placeholder="Password">
      <button class="auth-btn" on:click={() => submitFunction(key)}>Send</button>
    </div>
  </form>
</div>

<style lang=scss>
  .background {
    background-color: $darkest;
    padding: 1rem;
    border-radius: 10px;
    filter: drop-shadow(0 0 5px #00000098);
  }

  .container {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .auth-title {
    font-size: 22px;
    font-weight: 600;
    margin-bottom: 1rem;
  }

  .auth-btn {
    background-color: $dark;
    border: none;
    color: $white;
    padding: 0.5rem 1rem;

    &:hover {
      background-color: $darker;
    }
  }

  .auth-input {
    background-color: $dark;
    border: none;
    color: $white;
    padding: 0.5rem 1rem;
    margin-bottom: 0.5rem;
  }
</style>