<script>
  export let status;

  $: if (status) {
    console.log("Received status", status);
  }
</script>

{#if status && status.text}
  <div 
    class="notification"
    class:success={status.type == "success"}
    class:error={status.type == "error"}
    class:warning={status.type == "warning"}
  >
    <div class="notification-icon">
      {#if status.type && status.type == "success"}
        <i class="fa-solid fa-circle-check"></i>
      {:else if status.type && status.type == "error"}
        <i class="fa-solid fa-circle-xmark"></i>
      {:else if status.type && status.type == "warning"}
        <i class="fa-solid fa-circle-exclamation"></i>
      {/if}
    </div>
    <div class="notification-text">
      {status.text}
    </div>
  </div>
{/if}

<style lang="scss">
  .notification {
    display: flex;
    padding: 10px 20px;
    border-radius: 10px;
    align-items: center;
    margin-bottom: 20px;

    &-icon {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      margin-right: 20px;
    }

    &.error {
      background: #FF4E00;
    }

    &.success {
      background: #8EA604;
    }

    &.warning {
      background: #F5BB00;
    }
  }
</style>
