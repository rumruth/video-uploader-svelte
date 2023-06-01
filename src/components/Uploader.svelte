<script>
  import axios from 'axios';

  import Dragarea from './Dragarea.svelte';
  import Controls from './Controls.svelte';
  import Previews from './Previews.svelte';
  import Progress from './Progress.svelte';
  import Notif from './Notif.svelte';

  let files = [];
  let previewData = [];
  let uploading = false;
  let progress = 0;
  let success = false;
  let error = false;
  let status;

  function setStatus(data, time = 3000) {
    //console.log("Setting status...", data);
    status = data;

    setTimeout(() => {
      //console.log("Clearing status...");
      status = {}
    }, time);
  }

  function finishUploading() {
    files = [];
    uploading = false;
    progress = 0;
  }

  function tryUploading() {
    let form = new FormData();

    for (let i = 0; i < files.length; i++) {
      let file = files[i];
      form.append('uploads[]', file, file.name);
    }

    uploading = true;
    axios.request({
      method: "POST",
      url: `http://localhost:3000`,
      withCredentials: false,
      data: form,
      onUploadProgress: ProgressEvent => {
        progress = Math.round(ProgressEvent.loaded / ProgressEvent.total * 100);
      }
    }).then(data => {
      finishUploading();

      setStatus({
        text: "Successfully uploaded files!",
        type: "success"
      });
    }).catch(function (error) {
      console.log("Error?", error);

      finishUploading();

      setStatus({
        text: "Error uploading files!",
        type: "error"
      });
    });
  }
</script>

<div class="uploader">
  <div class="uploader-top"></div>
  <div class="uploader-inner">
    <div class="uploader-inner-title">
      {#if !uploading}
        Upload file
      {:else}
        Uploading...
      {/if}
    </div>

    <Notif {status} />

    {#if !uploading}
      <Dragarea bind:files />
      <Previews {files} />

      <Controls {files} on:submit={tryUploading} />
    {:else}
      <Progress {progress} />
    {/if}
  </div>
</div>

<style lang="scss">
  .uploader {
    border: 2px solid #15191C;
    border-bottom-right-radius: 10px;
    border-bottom-left-radius: 10px;
    border-top-right-radius: 10px;
    position: relative;

    &-top {
      border: 2px solid #15191C;
      border-bottom: 0px;
      border-top-left-radius: 10px;
      border-top-right-radius: 10px;
      background: #090E11;
      height: 20px;
      width: 30%;
      position: absolute;
      top: -20px;
      left: -2px;
      pointer-events: none;
      z-index: 2;
    }

    &-inner {
      padding: 0 20px 20px 20px;

      &-title {
        font-size: 26px;
        font-weight: 700;
        margin: -5px 0 30px 2px;
      }
    }
  }
</style>
