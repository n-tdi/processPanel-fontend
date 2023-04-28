<script>
  import { logUpdate } from "../../Stores.js";
  export let action;
  export let title;

  const sendAction = () => {
    fetch('http://localhost:8000/api/v1/poweraction/' + action + '?key=' + sessionStorage.getItem('auth'), {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      }
    })
    logUpdate.set(true);
  }
</script>

<button class="power-button" on:click={sendAction}>
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

