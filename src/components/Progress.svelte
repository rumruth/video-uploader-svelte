<script>
  export let progress = 0;
</script>

<div class="progress">
  <div class="progress-loader">
    <div class="lds-ripple">
      <div></div>
      <div></div>
    </div>
  </div>
  <div class="progress-bar">
    <div class="progress-bar-inner" style="width: {progress}%;"></div>
  </div>
</div>

<style lang="scss">
  .progress {
    &-loader {
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 10px 0 20px;
    }

    &-bar {
      width: 100%;
      border-radius: 10px;
      height: 20px;
      background: #15191C;
      position: relative;
      overflow: hidden;

      &-inner {
        background: #eceded;
        border-radius: 10px;
        height: 20px;
        position: absolute;
        left: 0;
        top: 0;
        bottom: 0;
        transition: all 0.2s ease-out;
      }
    }
  }

  .lds-ripple {
    display: inline-block;
    position: relative;
    width: 80px;
    height: 80px;

    div {
      position: absolute;
      border: 4px solid #fff;
      opacity: 1;
      border-radius: 50%;
      animation: lds-ripple 1s cubic-bezier(0, 0.2, 0.8, 1) infinite;

      &:nth-child(2) {
        animation-delay: -0.5s;
      }
    }
  }

  @keyframes lds-ripple {
    0% {
      top: 36px;
      left: 36px;
      width: 0;
      height: 0;
      opacity: 0;
    }
    4.9% {
      top: 36px;
      left: 36px;
      width: 0;
      height: 0;
      opacity: 0;
    }
    5% {
      top: 36px;
      left: 36px;
      width: 0;
      height: 0;
      opacity: 1;
    }
    100% {
      top: 0px;
      left: 0px;
      width: 72px;
      height: 72px;
      opacity: 0;
    }
  }
</style>
