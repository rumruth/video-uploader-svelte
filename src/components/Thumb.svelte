<script>
  export let thumb;
</script>

<div class="thumb">
  {#if thumb}
    <img src={thumb} />
  {:else}
    <div class="lds-ring"><div></div><div></div><div></div><div></div></div>
  {/if}
</div>

<style lang="scss">
  .thumb {
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    border: 2px solid #1D2125;
    width: 60px;
    height: 40px;
    background: #1D2125;
    border-radius: 5px;
    margin-right: 10px;

    img {
      min-height: 100%;
      min-height: 100%;
      align-self: center;
      object-fit: cover;
      width: 100%;
    }
  }

  .lds-ring {
    display: inline-block;
    position: relative;
    width: 20px;
    height: 20px;

    div {
      box-sizing: border-box;
      display: block;
      position: absolute;
      width: 14px;
      height: 14px;
      margin: 2px;
      border: 2px solid #fff;
      border-radius: 50%;
      animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
      border-color: #fff transparent transparent transparent;

      &:nth-child(1) {
        animation-delay: -0.45s;
      }

      &:nth-child(2) {
        animation-delay: -0.3s;
      }

      &:nth-child(3) {
        animation-delay: -0.15s;
      }
    }
  }

@keyframes lds-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

</style>
