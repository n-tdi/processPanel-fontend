<script>
    import Popup from "../cards/Popup.svelte";
    import EnvRow from "./ENVRow.svelte";

    let penvEnabled = true;
</script>

{#if !penvEnabled}
    <Popup title="Error" body="No Parent Environment set."/>
{:else}
    <EnvRow key="APP" value="TRUE"/>
    <EnvRow key="APP" value="TRUE"/>
    <EnvRow key="APP" value="TRUE"/>
    <EnvRow key="APP" value="TRUE"/>
{/if}

<style>

</style>