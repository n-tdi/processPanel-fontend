<script>
    import Popup from "../cards/Popup.svelte";
    import EnvRow from "./ENVRow.svelte";

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
</script>

{#if !penvEnabled}
    <Popup title="Error" body="No Parent Environment set."/>
{:else}
    {#each penv as env}
        <EnvRow key={env.key} value={env.value} removeFunction={remove} editFunction={edit} />
    {/each}
{/if}

<style>

</style>