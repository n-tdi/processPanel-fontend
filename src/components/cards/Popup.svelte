<script>
    export let title;
    export let body;
</script>

<div class="container">
    <h3 class="title">{title}</h3>
    <p class="body">{body}</p>
</div>

<style lang=scss>
    .container {
        background-color: $dark;
        border-radius: 10px;
        padding: 1rem;
        display: flex;
        flex-direction: column;
        justify-content: center;
        filter: drop-shadow(0 0 5px #00000098);
    }

    .title {
        margin-bottom: 0.5rem;
    }
</style>