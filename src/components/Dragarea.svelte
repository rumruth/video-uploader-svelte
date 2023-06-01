<script>
  export let files;
  let dragging = false;

  function handleFilesSelect(e) {
    dragging = false;

    const acceptedFiles = Array.from(e.dataTransfer.files);
    const acceptedItems = Array.from(e.dataTransfer.items);

    if (acceptedFiles.length > 0) {
      files = acceptedFiles;
    }
  }

  function handleFileChange(e) {
    //console.log("File change", files);
  }
</script>

<label
  for="dragfile"
  class="dragarea"
  class:dragging
  on:dragover|preventDefault={(e) => { dragging = true; }}
  on:dragleave|preventDefault={(e) => { dragging = false; }}
  on:drop|preventDefault={handleFilesSelect}
>
  <div class="dragarea-inner">
    <div class="dragarea-icon">
      <i class="fa-solid fa-file-arrow-up"></i>
    </div>
    <div class="dragarea-text">
      Drag and drop file here
    </div>
    <div class="dragarea-browse">
      or browse to choose a file
    </div>
  </div>
  <div class="dragarea-background">
    <div class="dragarea-background-spinner"></div>
  </div>
  <input type="file" id="dragfile" bind:files on:change={handleFileChange}>
</label>

<style lang="scss">
  .dragarea {
    overflow: hidden;
    position: relative;
    padding: 2px;
    border-radius: 10px;
    cursor: pointer;
    display: block;

    input {
      opacity: 0;
      position: absolute;
      left: 0;
      top: 0;
      z-index: 1;
      pointer-events: none;
    }

    &-inner {
      position: relative;
      z-index: 2;
      border: 2px dashed #1D2125;
      background: #15191C;
      border-radius: 10px;
      padding: 30px;
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
      transition: all 0.2s ease-out;
      pointer-events: none;
      width: 100%;
    }

    &.dragging {
      .dragarea-inner {
        background: #1D2125;
        border-color: transparent;
      }

      .dragarea-background {
        opacity: 1;
      }
    }

    &:hover {
      .dragarea-inner {
        background: #1D2125;
      }
    }

    &-background {
      position: absolute;
      pointer-events: none;
      top: 0;
      right: 0;
      left: 0;
      bottom: 0;
      z-index: 1;
      overflow: hidden;
      opacity: 0;
      transition: opacity 0.2s ease-out;

      &-spinner {
        background-image: repeating-conic-gradient(#ECECEC 0deg 10deg, #1D2125 10deg 20deg);
        animation: rotating 8s linear infinite;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 110%;
        padding-top: 110%;
      }
    }

    &-icon {
      font-size: 60px;
      margin-bottom: 20px;
    }

    &-text {
      margin-bottom: 5px;
      font-size: 20px;
    }
  }

  @keyframes rotating {
    from {
      -ms-transform: translate(-50%, -50%) rotate(0deg);
      -moz-transform: translate(-50%, -50%) rotate(0deg);
      -webkit-transform: translate(-50%, -50%) rotate(0deg);
      -o-transform: translate(-50%, -50%) rotate(0deg);
      transform: translate(-50%, -50%) rotate(0deg);
    }
    to {
      -ms-transform: translate(-50%, -50%) rotate(360deg);
      -moz-transform: translate(-50%, -50%) rotate(360deg);
      -webkit-transform: translate(-50%, -50%) rotate(360deg);
      -o-transform: translate(-50%, -50%) rotate(360deg);
      transform: translate(-50%, -50%) rotate(360deg);
    }
  }
</style>
