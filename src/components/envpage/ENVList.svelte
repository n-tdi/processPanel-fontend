<script>
  import Popup from "../cards/Popup.svelte";
  import EnvRow from "./ENVRow.svelte";
  import { browser } from '$app/environment';
  import { PUBLIC_API_URL } from '$env/static/public'
  import { logUpdate } from "../../Stores.js";

  let addKey = "";
  let addValue = "";

  let penvEnabled;
  let penv = [];

  fetch(PUBLIC_API_URL + 'penv/has', {
    method: 'GET',
    headers: {
      'Content-Type': 'application/json'
    }
  }).then(res => res.json()).then(res => {
    penvEnabled = res.response;
    if (penvEnabled && browser) {
      fetch(PUBLIC_API_URL + 'penv/get?key=' + sessionStorage.getItem('auth'), {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json'
        }
      }).then(res => res.json()).then(res => {
        penv = res.response;
      });
    }
  });

  const remove = (key) => {
    penv = penv.filter(env => env.key !== key);
    fetch(PUBLIC_API_URL + 'penv/remove?key=' + sessionStorage.getItem('auth') + '&key1=' + key, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      }
    })
    logUpdate.set(true);
  };

  const edit = (key, value) => {
    penv = penv.map(env => {
      if (env.key === key) {
        env.value = value;
      }
      return env;
    });
    fetch(PUBLIC_API_URL + 'penv/update?key=' + sessionStorage.getItem('auth') + '&key1=' + key + '&value=' + value, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      }
    })
    logUpdate.set(true);
  };

  const add = (key, value) => {
    penv = penv.filter(env => env.key !== key);
    if (key !== "" && value !== "") penv = [...penv, {key: key, value: value}];
    addKey = "";
    addValue = "";
    fetch(PUBLIC_API_URL + 'penv/add?key=' + sessionStorage.getItem('auth') + '&key1=' + key + '&value=' + value, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      }
    })
    logUpdate.set(true);
  }
</script>

{#if !penvEnabled}
    <Popup title="Error" body="No Parent Environment set."/>
{:else}
    <div class="env-header">
      <h4 class="key-header">KEY</h4>
      <h4 class="value-header">VALUE</h4>
    </div>
    {#each penv as env}
        <EnvRow key={env.key} value={env.value} removeFunction={remove} editFunction={edit} />
    {/each}
    <div class="addition">
      <form class="sb" on:submit|preventDefault={() => add(addKey, addValue)}>
        <input type="text" name="key" id="key" class="key" placeholder="Key" bind:value={addKey}>
        <input type="text" name="value" id="value" class="value" placeholder="Value" bind:value={addValue}>
        <button class="hide"></button>
      </form>
    </div>
{/if}

<style lang=scss>
  .env-header {
    display: flex;
    justify-content: space-between;
    padding: 0 0 8px 0;
  }

  .addition {
    display: flex;
    flex-direction: column;
    padding: 8px 0;
  }

  .sb {
    display: flex;
    justify-content: space-between;
  }

  .key, .value {
    border: none;
    background-color: $darkest;
    color: white;
    border-left: 1px solid $dark;
    border-right: 1px solid $dark;
    padding-left: 4px;
  }

  .bottom {
    display: flex;
    justify-content: center;
  }

  .add-btn {
    background-color: $darkest;
    border: none;
    color: white;
    font-size: 1rem;
    font-weight: 800;
    cursor: pointer;
  }

  .hide {
    display: none;
  }
</style>