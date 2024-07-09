
<script>
  import { onMount } from "svelte";
  import { createEventDispatcher } from "svelte";

  export let textId;
  export let content = "An intuitive tool for";
  export let font = "Abyssinica SIL";
  export let style = "regular";
  export let size = 3.664328;
  export let letter = 0;
  export let line = 1;
  export let align = "left";
  export let color = "#294958";

  // Shadow properties
  export let colorShadow = "#000000";
  export let opacity = 1;
  export let blur = 0;
  export let offsetX = 0;
  export let offsetY = 0;

  let fonts = [];
  let isDropdownOpen = false;
  let isLoading = true;
  let error = null;

  const dispatch = createEventDispatcher();

  onMount(async () => {
  try {
    const response = await fetch('src/routes/(tools)/app-store-screenshot-generator/api/fonts/+server.js');
    const data = await response.json();
    fonts = data.items;
    isLoading = false;
  } catch (err) {
    error = 'Failed to load fonts';
    isLoading = false;
  }
});


  function updateText() {
    dispatch("update", {
      id: textId,
      content,
      font,
      style,
      size,
      letter,
      line,
      align,
      color,
      colorShadow,
      opacity,
      blur,
      offsetX,
      offsetY,
    });
  }

  function toggleDropdown() {
    isDropdownOpen = !isDropdownOpen;
  }
</script>

<div class="mb-1">
  <h3 class="text-lg font-extrabold text-gray-700 mb-2">Text</h3>

  <div class="mb-1">
    <label for="content" class="block text-xs text-gray-500">Content</label>
    <input
      id="content"
      type="text"
      bind:value={content}
      on:input={updateText}
      class="mt-1 block w-full text-xs"
    />
  </div>

  <div class="mb-1">
    <label for="font" class="block text-xs text-gray-500">Font</label>
    <select
      id="font"
      bind:value={font}
      on:change={updateText}
      class="mt-1 block w-full text-xs"
    >
      {#if isLoading}
        <option>Loading...</option>
      {:else if error}
        <option>{error}</option>
      {:else}
        {#each fonts as fontOption}
          <option value={fontOption.family}>{fontOption.family}</option>
        {/each}
      {/if}
    </select>
  </div>

  <div class="mb-1">
    <label for="style" class="block text-xs text-gray-500">Style</label>
    <select
      id="style"
      bind:value={style}
      on:change={updateText}
      class="mt-1 block w-full text-xs"
    >
      <option value="regular">Regular</option>
      <option value="italic">Italic</option>
      <option value="bold">Bold</option>
      <option value="bold italic">Bold Italic</option>
    </select>
  </div>

  <div class="mb-1">
    <label for="size" class="block text-xs text-gray-500">Size</label>
    <input
      id="size"
      type="range"
      min="0"
      max="10"
      step="0.000001"
      bind:value={size}
      on:input={updateText}
      class="mt-1 block w-full"
    />
  </div>

  <div class="mb-1">
    <label for="letter" class="block text-xs text-gray-500">Letter Spacing</label>
    <input
      id="letter"
      type="range"
      min="-5"
      max="5"
      step="0.1"
      bind:value={letter}
      on:input={updateText}
      class="mt-1 block w-full"
    />
  </div>

  <div class="mb-1">
    <label for="line" class="block text-xs text-gray-500">Line Height</label>
    <input
      id="line"
      type="range"
      min="0.5"
      max="3"
      step="0.1"
      bind:value={line}
      on:input={updateText}
      class="mt-1 block w-full"
    />
  </div>

  <div class="mb-1">
    <label for="color" class="block text-xs text-gray-500">Color</label>
    <input
      id="color"
      type="color"
      bind:value={color}
      on:input={updateText}
      class="mt-1 block w-full h-6"
    />
  </div>

  <h3 class="text-lg font-extrabold text-gray-700 mb-1">Shadow</h3>
  <div class="mb-1">
    <label for="colorShadow" class="block text-xs text-gray-500">Color</label>
    <input
      id="colorShadow"
      type="color"
      bind:value={colorShadow}
      on:input={updateText}
      class="mt-1 block w-full h-6"
    />

    <label for="opacity" class="block text-xs text-gray-500 mt-1">Opacity</label>
    <input
      id="opacity"
      type="range"
      min="0"
      max="1"
      step="0.01"
      bind:value={opacity}
      on:input={updateText}
      class="mt-1 block w-full"
    />

    <label for="blur" class="block text-xs text-gray-500 mt-1">Blur</label>
    <input
      id="blur"
      type="range"
      min="0"
      max="50"
      step="1"
      bind:value={blur}
      on:input={updateText}
      class="mt-1 block w-full"
    />

    <label for="offsetX" class="block text-xs text-gray-500 mt-1">Offset X</label>
    <input
      id="offsetX"
      type="range"
      min="-50"
      max="50"
      step="1"
      bind:value={offsetX}
      on:input={updateText}
      class="mt-1 block w-full"
    />

    <label for="offsetY" class="block text-xs text-gray-500 mt-1">Offset Y</label>
    <input
      id="offsetY"
      type="range"
      min="-50"
      max="50"
      step="1"
      bind:value={offsetY}
      on:input={updateText}
      class="mt-1 block w-full"
    />
  </div>
  <div>
    <button class="mt-4 px-4 py-1 bg-black text-white text-s rounded">Delete Element</button>
  </div>
</div>