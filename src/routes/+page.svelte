<script>
  import { browser } from '$app/environment';
  import { PUBLIC_API_URL } from '$env/static/public'
  import Card from "../components/cards/Card.svelte";
  import EnvList from "../components/envpage/ENVList.svelte";
  import SignIn from '../components/cards/SignIn.svelte';
  import LogArea from '../components/logpage/LogArea.svelte';

  let signedIn;

  if (browser) {
    signedIn = sessionStorage.getItem('auth');
  }

  const submit = (key) => {
    if (key !== '') {
      fetch(PUBLIC_API_URL + 'login/checkkey?key=' + key, {
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

<svelte:head>
    <title>Process Panel - Ntdi World</title> 
</svelte:head>


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

