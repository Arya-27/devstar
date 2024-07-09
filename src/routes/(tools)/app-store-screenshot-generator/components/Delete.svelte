 // Arya's Component
 <script>
  import { createEventDispatcher } from 'svelte';
 

  const dispatch = createEventDispatcher();
  let showBackgroundCustomizer = false;
  let selectedDevice = null; // Track the selected device
  let fileInput;
  let devices = []; 

  function handleClick(action) {
    if (action === 'changeBackground') {
      showBackgroundCustomizer = !showBackgroundCustomizer;
    } else if (action === 'addImage') {
      fileInput.click();
    } else if (action === 'deleteDevice') {
      deleteDevice();
    } else {
      dispatch('action', { type: action });
    }
  }

  function handleFileChange(event) {
    const file = event.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = (e) => {
        dispatch('action', { type: 'addImage', payload: e.target.result });
      };
      reader.readAsDataURL(file);
    }
  }

  const navItems = [
    { action: 'deleteDevice', name: '', icon: 'M9 3v1H4v2h16V4h-5V3H9zm1 4v12h2V7h-2zM6 8v12h2V8H6zm10 0v12h2V8h-2z' }, 
  ];

  function handleBackgroundUpdate(event) {
    const background = event.detail;
    dispatch('backgroundUpdate', background);
  }

  function selectDevice(device) {
    selectedDevice = device;
  }

  function deleteDevice() {
    if (selectedDevice) {
      devices = devices.filter(d => d !== selectedDevice);
      selectedDevice = null; // Reset selected device after deletion
    }
  }

  $: if (selectedDevice) {
    console.log('Selected device:', selectedDevice);
  }
</script>

<div>
  <nav>
    {#each navItems as navItem}
      <button on:click={() => handleClick(navItem.action)}>
        <svg>{@html navItem.icon}</svg>
        {navItem.name}
      </button>
    {/each}
  </nav>

  {#if showBackgroundCustomizer}
    <!-- svelte-ignore missing-declaration -->
    <BackgroundCustomizer on:backgroundUpdate={handleBackgroundUpdate} />
  {/if}

  <input type="file" bind:this={fileInput} on:change={handleFileChange} style="display: none;" />

  <ul>
    {#each devices as device}
      
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <li on:click={() => selectDevice(device)} class:selected={device === selectedDevice}>
        {device.name}
      </li>
    {/each}
  </ul>
</div>

<style>
  .selected {
    background-color: lightblue;
  }
</style>
