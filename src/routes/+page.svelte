<script>
  import { browser } from '$app/environment';
  import Card from "../components/cards/Card.svelte";
  import EnvList from "../components/envpage/ENVList.svelte";
  import SignIn from '../components/cards/SignIn.svelte';
  import LogArea from '../components/logpage/LogArea.svelte';

  export let data;

  let signedIn;

  if (browser) {
    signedIn = sessionStorage.getItem('auth');
  }

  const submit = (key) => {
    if (key !== '') {
      fetch('http://localhost:8000/api/v1/login/checkkey?key=' + key, {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json'
        }
      }).then(res => res.json()).then(res => {
        if (res.response === "correct") {
          sessionStorage.setItem('auth', key);
          signedIn = true;
        } else {
          signedIn = false;
        }
      });
    }
  }
</script>

{#if signedIn}
<div class="cards-2">
    <div class="cards-left side-card">
        <Card title="Environment Variables">
            <EnvList />
        </Card>
    </div>
    <div class="cards-right side-card">
        <Card title="Logs">
          <LogArea />
        </Card>
    </div>
</div>
{:else}
<SignIn submitFunction={submit} />
{/if}

<style lang=scss>
  .cards-2 {
    display: flex;
    flex-wrap: wrap;
  }

  .cards-left {
    flex: 2;
    margin-right: 2rem;
  }

  .cards-right {
    flex: 3;
  }
</style>

