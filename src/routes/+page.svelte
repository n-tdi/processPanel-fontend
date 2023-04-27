<script>
  import Card from "../components/cards/Card.svelte";
  import EnvList from "../components/envpage/ENVList.svelte";
</script>

<div class="cards-2">
    <div class="cards-left side-card">
        <Card title="Environment Variables">
            <EnvList />
        </Card>
    </div>
    <div class="cards-right side-card">
        <Card title="Logs">
        </Card>
    </div>
</div>

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

