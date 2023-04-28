<script>
  export let key;
  export let value;
  export let removeFunction;
  export let editFunction;
    
  let editing = false;

  const toggleEdit = () => {
    if (editing) {
      editFunction(key, value);
    }
    editing = !editing;
  }
</script>

<div class="container">
  <p class="key">{key}</p>
  <div class="info">
      <button class="info-btn" on:click={() => {removeFunction(key)}}>Remove</button>
  </div>
  <div class="value-div">
    {#if !editing}
      <p class="value" on:click={toggleEdit}>{value}</p>
    {:else}
      <form on:submit|preventDefault={toggleEdit}>
        <input type="text" on:focusout={toggleEdit} name="edit" id="edit" class="edit" bind:value={value}>
      </form>
    {/if}
  </div>
</div>

<style lang=scss>
    .container {
        display: flex;
        justify-content: space-between;
        border-bottom: 1px solid $dark;
        padding: 8px 0;
        transition: all 0.1s ease-in-out;
        &:hover {
            .info {
                opacity: 100%;
                display: flex;
                align-items: center;
                justify-content: space-around;
                gap: 1rem;
            }
        }
    }

    .key .value {
        font-weight: 400;
    }

    .value {
      cursor: pointer;
    }

    .info {
        opacity: 0%;
        transition: all 0.2s ease-in-out;
    }

    .info-btn {
        border: none;
        background-color: $darkest;
        color: $white;
        cursor: pointer;
    }

    .edit {
      border: none;
      border-left: 1px solid $dark;
      border-right: 1px solid $dark;
      background-color: $darkest;
      color: $white;
      padding: 0 6px;
    }
</style>