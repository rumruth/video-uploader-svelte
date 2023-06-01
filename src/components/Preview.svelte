<script>
  import Thumb from './Thumb.svelte';

  export let preview;
</script>

<div class="preview">
  {#if preview}
    <Thumb thumb={preview.thumb} />
    <div class="preview-title">
      {preview.name}
    </div>
    <div class="preview-size">
      {preview.size}
    </div>
  {/if}
</div>

<style lang="scss">
  .preview {
    border-radius: 10px;
    background: #15191C;
    margin-bottom: 10px;
    padding: 10px;
    display: flex;
    align-items: center;

    &-title {
      font-weight: 600;
      margin-right: 20px;
    }

    &:last-child {
      margin-bottom: 0;
    }
  }
</style>
