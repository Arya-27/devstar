<!--Vaishnavi's part(Download Button)-->
<script>
  let fileType = 'JPG';
  let size = 1;
  let quality = 80;
  let width = 1024;
  let height = 768;
  let saveSettings = false;
  let showSettings = false;

  function toggleSettings() {
    showSettings = !showSettings;
  }

  function download() {
    const canvas = document.createElement('canvas');
    canvas.width = Math.round(width * size);
    canvas.height = Math.round(height * size);
    const ctx = canvas.getContext('2d');

    ctx.fillStyle = '#6C63FF';
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    const dataURL = canvas.toDataURL(`image/${fileType.toLowerCase()}`, quality / 100);

    const link = document.createElement('a');
    link.href = dataURL;
    link.download = `download.${fileType.toLowerCase()}`;
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);

    showSettings = false;
  }
</script>

<svelte:head>
  <style>
    /* No need for inline styles */
  </style>
</svelte:head>

<div class="container p-4 font-sans flex flex-col items-center relative">
  <button class="download-btn bg-indigo-600 text-white py-2 px-4 rounded mb-[-3rem] ml-auto" on:click={toggleSettings}>Download</button>


  {#if showSettings}
  <div class="card absolute top-full right-0 w-72 p-4 border border-gray-300 rounded bg-white shadow-md z-10 mt-8">
      <label class="mb-2 block">
        File type
        <select bind:value={fileType} class="border rounded px-2 py-1 mt-2">
          <option value="JPG">JPG</option>
          <option value="PNG">PNG</option>
          <option value="GIF">GIF</option>
        </select>
      </label>

      <div class="slider mb-2">
        <label class="block">
          Size
          <input type="range" min="0.1" max="2" step="0.1" bind:value={size} class="my-2" />
          <span>{Math.round(width * size)} x {Math.round(height * size)} px</span>
        </label>
      </div>

      <div class="slider mb-2">
        <label class="block">
          Quality
          <input type="range" min="1" max="100" step="1" bind:value={quality} class="my-2" />
        </label>
        <span>{quality}</span>
      </div>

      <label class="block mb-2">
        <input type="checkbox" bind:checked={saveSettings} class="mr-2" />
        Save download settings
      </label>

      <button class="confirm-btn bg-green-500 text-white py-2 px-4 rounded w-1/2" on:click={download}>Confirm</button>
    </div>
  {/if}
</div>
<!--Vaishnavi's part(Download Button)End-->
