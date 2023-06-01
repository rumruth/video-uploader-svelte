<script>
  import Preview from './Preview.svelte';

  export let files = [];

  let previewData = [];

  function formatBytes(bytes, decimals = 2) {
    if (!+bytes) return '0 Bytes'

    const k = 1024
    const dm = decimals < 0 ? 0 : decimals
    const sizes = ['Bytes', 'KiB', 'MiB', 'GiB', 'TiB', 'PiB', 'EiB', 'ZiB', 'YiB']

    const i = Math.floor(Math.log(bytes) / Math.log(k))

    return `${parseFloat((bytes / Math.pow(k, i)).toFixed(dm))} ${sizes[i]}`
  }

  function processThumbnails (fileArray, i) {
    if (!fileArray[i]) return;

    let file = fileArray[i];

    let fileReader = new FileReader();
    fileReader.onload = function() {
      console.log("file reader loaded");

      let blob = new Blob([fileReader.result], {type: file.type});
      let url = URL.createObjectURL(blob);
      let video = document.createElement('video');
      let timeupdate = function() {
        if (snapImage()) {
          video.removeEventListener('timeupdate', timeupdate);
          video.pause();
        }
      };

      video.addEventListener('loadeddata', function() {
        if (snapImage()) {
          video.removeEventListener('timeupdate', timeupdate);
        }
      });

      let snapImage = function() {
        let canvas = document.createElement('canvas');
        canvas.width = video.videoWidth;
        canvas.height = video.videoHeight;
        canvas.getContext('2d').drawImage(video, 0, 0, canvas.width, canvas.height);
        let image = canvas.toDataURL();
        let success = image.length > 100000;
        if (success) {

          previewData[i].thumb = image;

          processThumbnails(fileArray, i+1);

          video.remove();
          canvas.remove();

          URL.revokeObjectURL(url);
        }
        return success;
      };

      video.addEventListener('timeupdate', timeupdate);
      video.preload = 'metadata';
      video.src = url;
      // Load video in Safari / IE11
      video.muted = true;
      video.playsInline = true;
      video.play();
    };
    fileReader.readAsArrayBuffer(file);
  }

  function processPreviews() {
    console.log("processing previews");

    for (let i = 0; i < files.length; i++) {
      console.log(files[i]);
      previewData.push({
        name: files[i].name,
        size: formatBytes(files[i].size)
      });
    }

    let tempFiles = files;

    processThumbnails(tempFiles, 0);
  }

  $: {
    if (files && files.length > 0) {
      console.log("Processing previews");
      processPreviews();
    }
  }
</script>

{#if previewData.length > 0}
  <div class="previews">
    {#each previewData as preview, i}
      <Preview {preview} />
    {/each}
  </div>
{/if}

<style lang="scss">
  .previews {
    padding: 10px 0px 0px;
  }
</style>
