<script>
    export let key;
    export let value;

</script>

<div class="container">
    <p class="key">{key}</p>
    <div class="info">
        <button class="info-btn">Edit</button>
        <button class="info-btn">Remove</button>
    </div>
    <p class="value">{value}</p>
</div>

<style lang=scss>
    .container {
        display: flex;
        justify-content: space-between;
        border-bottom: 1px solid $dark;
        padding: 8px 0;

        &:hover {
            .info {
                display: flex;
                align-items: center;
                justify-content: space-around;
                gap: 1rem;
            }
        }
    }

    .key, .value {
        font-weight: 400;
    }

    .info {
        display: none;
    }

    .info-btn {
        border: none;
        background-color: $darkest;
        color: $white;
    }
</style>