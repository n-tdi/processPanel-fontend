<script>
  import Card from "../components/cards/Card.svelte";
  import PowerButtonList from "../components/poweraction/PowerButtonList.svelte";
</script>

<div class="cards">
  <div class="cards-top">
    <div class="cards-top_child">
      <Card title="Enviornment Variables">
      </Card>
    </div>
  </div>
  <div class="cards-bottom">
    <Card title="Logs">
    </Card>
  </div>
</div>

<style lang=scss>
  .cards {
    display: flex;
    flex-direction: column;
  }
  .cards-top {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
  }
  .cards-top_child {
    flex: 1;
  }

</style>

