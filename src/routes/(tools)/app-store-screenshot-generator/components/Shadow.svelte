
/* Arya's Component- Shadow functionality and Delete Element */
<script>
  import Delete from "./Delete.svelte";

  let shadowColor = "#000000";
  let shadowOpacity = 1;
  let shadowBlur = 0;
  let offsetX = 0;
  let offsetY = 0;

  $: boxShadow = `${offsetX}px ${offsetY}px ${shadowBlur}px rgba(${parseInt(shadowColor.slice(1, 3), 16)}, ${parseInt(shadowColor.slice(3, 5), 16)}, ${parseInt(shadowColor.slice(5, 7), 16)}, ${shadowOpacity})`;

</script>

<div class="container">
  <span class="title">Shadow</span>
  <div class="settings">
    <div class="row">
      <span>Color</span>
      <div class="color-container">
        <input type="color" bind:value={shadowColor} class="color" />
        <input type="text" bind:value={shadowColor} class="box1" />
      </div>
    </div>
    <div class="row">
      <span>Opacity</span>
      <div class="shadow-container">
        <input
          type="number"
          bind:value={shadowOpacity}
          min="0"
          max="1"
          class="box"
        />
        <input
          type="range"
          bind:value={shadowOpacity}
          min="0"
          max="1"
          step="0.01"
          class="slider"
        />
      </div>
    </div>
    <div class="row">
      <span>Blur</span>
      <div class="shadow-container">
        <input
          type="number"
          bind:value={shadowBlur}
          min="0"
          max="10"
          step="0.05"
          class="box"
        />
        <input
          type="range"
          bind:value={shadowBlur}
          min="0"
          max="10"
          step="0.05"
          class="slider"
        />
      </div>
    </div>
    <div class="row">
      <span>Offset X</span>
      <div class="shadow-container">
        <input
          type="number"
          bind:value={offsetX}
          min="-10"
          max="10"
          step="0.001"
          class="box"
        />
        <input
          type="range"
          bind:value={offsetX}
          min="-10"
          max="10"
          step="0.001"
          class="slider"
        />
      </div>
    </div>
    <div class="row">
      <span>Offset Y</span>
      <div class="shadow-container">
        <input
          type="number"
          bind:value={offsetY}
          min="-10"
          max="10"
          step="0.001"
          class="box"
        />
        <input
          type="range"
          bind:value={offsetY}
          min="-10"
          max="10"
          step="0.001"
          class="slider"
        />
      </div>
    </div>
    <div class="preview" style="--box-shadow: {boxShadow};"></div>
    <button class="mt-2 px-3 py-1 bg-black text-white rounded text-xs">Delete Element</button>
    <Delete/>
  </div>
</div>

<style>
  .container {
    margin-bottom: 1rem;
  }
  .title {
    font-weight: bold;
    font-size: larger;
  }
  .settings {
    display: flex;
    flex-direction: column;
  }
  .row {
    display: flex;
    align-items: center;
    margin-bottom: 1rem;
  }
  .shadow-container {
    display: flex;
    align-items: center;
    margin-left: auto;
  }
  .color-container {
    display: flex;
    align-items: center;
    margin-left: auto;
  }
  .slider {
    margin-left: 0.5rem;
    width: 85px;
    margin-right: 0.5rem;
  }
  .color {
    margin-left: 0.5rem;
    width: 78px;
    height: 40px;
    margin-right: 0.5rem;
    border: 2px solid whitesmoke;
    border-radius: 10px;
  }
  .box,
  .box1 {
    margin-left: 0.5rem;
    width: 90px;
    height: 40px;
    margin-right: 0.5rem;
    border: 2px solid whitesmoke;
    border-radius: 10px;
    font-size: smaller;
  }
  .preview {
    width: 100px;
    height: 100px;
    background-color: white;
    box-shadow: var(--box-shadow);
  }
</style>

 