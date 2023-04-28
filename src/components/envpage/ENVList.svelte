<script>
    import Popup from "../cards/Popup.svelte";
    import EnvRow from "./ENVRow.svelte";

    let addKey = "";
    let addValue = "";

    let penvEnabled = true;

    let penv = [
        {key: "APP", value: "TRUE"},
        {key: "COOL", value: "TRUE"},
        {key: "REAL", value: "TRUE"}
    ];

    const remove = (key) => {
        penv = penv.filter(env => env.key !== key);
        console.log("Calling API on " + key);
    };

    const edit = (key, value) => {
        penv = penv.map(env => {
            if (env.key === key) {
                env.value = value;
            }
            return env;
        });
        console.log("Editing " + key + " to " + value);
    };

    const add = (key, value) => {
      penv = penv.filter(env => env.key !== key);
      if (key !== "" && value !== "") penv = [...penv, {key: key, value: value}];
      addKey = "";
      addValue = "";
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