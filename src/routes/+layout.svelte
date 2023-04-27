<script>
  import '../app.scss';
  import Navbar from '../components/Navbar.svelte';
</script>
<Navbar title="Process Panel" />
<div class="container">
  <slot></slot>
</div>

<style lang=scss>
  .container {
    max-width: $max-width;
    margin: 0 auto;
    margin-top: 2.5rem;
  }
</style>