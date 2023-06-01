<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  export let files;

  function submit() {
    dispatch('submit');
  }

</script>

{#if files.length > 0}
  <div class="controls">
    <button on:click|once={submit}>Submit</button>
  </div>
{/if}

<style lang="scss">
  .controls {
    display: flex;
    padding: 10px 0 0;
    justify-content: flex-end;

    button {
      border-radius: 10px;
      background: #15191C;
      margin-bottom: 10px;
      border: 0px;
      color: #eceded;
      font-size: 15px;
      font-weight: 600;
      padding: 10px 14px;
      display: inline;
      justify-content: center;
      align-items: center;
      cursor: pointer;
      transition: all 0.2s ease-out;

      &:hover {
        background: #1D2125;
      }
    }
  }
</style>
