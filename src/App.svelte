<script>
  import Uploader from './components/Uploader.svelte';
</script>

<main>
  <div class="container">
    <Uploader />
  </div>
</main>

<style lang="scss">
  main {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    flex-direction: column;
    align-items: center;

    &:before,
    &:after {
      content: "";
      width: 100%;
      flex-grow: 1;
      min-height: 20px;
    }
  }
</style>
