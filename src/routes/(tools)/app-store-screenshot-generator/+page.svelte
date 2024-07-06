<!--Adin's part(Device)-->
<script>
    let files = null;
    let items = [
        "Dynamic Frame", "Apple Display XDR", "Apple Watch Closed", "Apple Watch Open",
        "Chrome 1080p", "Chrome 1440p", "Chrome 720p", "Google Pixel 4", "iPad Air 3rd Gen",
        "iPad Pro Clay", "iPad Pro Real", "iPhone 11 Clay", "iPhone 11 Clay Thin", 
        "iPhone 11 Real", "iPhone 12 Multicolor", "iPhone 12 Real", "iPhone 13 Pro",
        "iPhone 13 Pro Max", "iPhone 8 Real", "MacBook Pro Clay", "MacBook Pro Real",
        "Safari 1080p", "Safari 1440p", "Safari 720p", "Samsung S10", "Samsung S20",
        "Samsung TV", "Smart TV", "Surface Pro Book", "Surface Pro Tablet"
    ];
    let selectedItem = "iPhone 11 Clay Thin";
    let isOpen = false;
    let isColorPopupOpen = false;
    let selectedColor = 'darkblue';
    let colors = [
        { color: "white", borderColor: "lightgray" },
        { color: "lightsalmon", borderColor: "#e9967a" },
        { color: "lightblue", borderColor: "#4682b4" },
        { color: "lightpink", borderColor: "#db7093" },
        { color: "darkblue", borderColor: "#00008b" },
        { color: "lightgreen", borderColor: "#32cd32" },
        { color: "black", borderColor: "black" },
        { color: "red", borderColor: "#b20000" }
    ];
    let sliderValue = 0;

    function toggleDropdown() {
        isOpen = !isOpen;
    }

    function selectItem(item) {
        selectedItem = item;
        isOpen = false;
    }

    function toggleColorPopup() {
        isColorPopupOpen = !isColorPopupOpen;
    }

    function selectColor(color) {
        selectedColor = color;
        isColorPopupOpen = false;
    }

    function closeColorPopup() {
        isColorPopupOpen = false;
    }

    function updateSliderFromTextbox(event) {
        let value = parseFloat(event.target.value);
        if (!isNaN(value)) {
            if (value > 200) {
                sliderValue = 200;
            } else if (value < 0) {
                sliderValue = 0;
            } else {
                sliderValue = value;
            }
        } else {
            sliderValue = 0;
        }
        updateTextboxFromSlider(sliderValue);
    }

    function updateSliderFromRange(event) {
        sliderValue = parseFloat(event.target.value);
        document.querySelector('.slider-value-box').value = sliderValue;
    }

    function updateTextboxFromSlider(value) {
        document.querySelector('.slider-value-box').value = value;
    }
</script>

<div class="card gap-16 items-center mx-auto max-w-screen-xl lg:grid lg:grid-cols-2 overflow-hidden rounded-lg">
    <div>
        <h1 class="font-bold text-xl px-4 mt-5 mb-3">Device</h1>
        <!-- Screenshot -->
        <div class="mb-2 flex justify-between items-center">
            <h1 class="ml-10 font-semibold whitespace-nowrap text-gray-800">Screenshot</h1>
            <label for="image-input" class="mx-auto ml-4 border border-gray-300 px-10 py-2 rounded-md bg-gray-200 hover:bg-gray-400 whitespace-nowrap flex justify-between items-center" style="width: 175px;">
                <div>
                    {#if files && files.length}
                        <p>{files[0].name}</p>
                    {:else}
                        <p>Choose file</p>
                    {/if}
                </div>
            </label>
            <input bind:files id="image-input" name="image" type="file" accept="image/jpeg,image/png" class="hidden" required>
        </div>

        <!-- Frame -->
        <div class="mb-2 flex justify-between items-center">
            <h1 class="ml-10 font-semibold text-gray-800">Frame</h1>
            <div class="dropdown mx-auto ml-14">
                <input type="text" class="textbox rounded-md px-1 py-2 bg-gray-50 border border-gray-200" value={selectedItem} on:click={toggleDropdown} readonly style="width: 175px; height: 35px; cursor: pointer;">
                <div class="option {isOpen ? 'show' : ''}">
                    {#each items as item}
                        <div on:click={() => selectItem(item)}>{item}</div>
                    {/each}
                </div>
            </div>
        </div>

        <!-- Color -->
        <div class="mb-4 flex justify-between items-center relative">
            <h1 class="px-10 mb-2 mt-2 font-semibold text-gray-800">Color</h1>
            <div class="color-block rounded-md bg-gray-100 mx-auto ml-6 flex justify-center items-center" style="width: 75px; height: 35px; cursor: pointer;" on:click={toggleColorPopup}>
                <div class="inner-color rounded-md" style="width: 80%; height: 60%; background-color: {selectedColor};"></div>
            </div>
            <div class="color-popup {isColorPopupOpen ? 'show' : ''}">
                <span class="close-btn" on:click={closeColorPopup}>&times;</span>
                <h2 class="font-semibold mb-2">Color</h2>
                {#each colors as {color, borderColor}}
                    <div class="color-option" style="background-color: {color}; border-color: {borderColor};" on:click={() => selectColor(color)}></div>
                {/each}
            </div>
        </div>

        <!-- Size -->
        <div class="mb-2 flex justify-between items-center">
            <h1 class="px-10 mb-3 font-semibold text-gray-800">Size</h1>
            <div class="slider-container mx-auto ml-4 flex items-center">
                <input type="text" value={sliderValue} on:input={updateSliderFromTextbox} class="slider-value-box ml-5 p-1 bg-gray-100 border border-gray-200 rounded-md" style="width: 75px;">
                <input type="range" min="0" max="200" value={sliderValue} on:input={updateSliderFromRange} class="slider">
            </div>
        </div>
    </div>
</div>

<style>
    .dropdown {
        position: relative;
    }

    .textbox {
        width: 165px;
        height: 30px;
        cursor: pointer;
        padding-right: 20px;
    }

    .dropdown::after {
        content: '▼';
        position: absolute;
        right: 10px;
        top: 50%;
        transform: translateY(-50%);
        pointer-events: none;
    }

    .option {
        display: none;
        position: absolute;
        background: white;
        border: 1px solid #ccc;
        width: 100%;
        max-height: 200px;
        overflow-y: auto;
        z-index: 1000;
    }

    .option div {
        padding: 2px;
        cursor: pointer;
    }

    .option div:hover {
        background-color: #f0f0f0;
    }

    .show {
        display: block;
    }

    .inner-color {
        background-color: darkblue;
    }

    .color-popup {
        display: none;
        position: absolute;
        top: -60px;
        left: 70%;
        transform: translateX(-50%);
        background: white;
        border: 1px solid #ccc;
        padding: 10px;
        border-radius: 10px;
        z-index: 1000;
        box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
        width: 290px;
        height: auto;
    }

    .color-popup.show {
        display: block;
    }

    .color-option {
        width: 38px;
        height: 38px;
        margin: 3px;
        display: inline-block;
        cursor: pointer;
        border-radius: 5px;
        border: 2px solid;
    }

    .close-btn {
        position: absolute;
        top: 1px;
        right: 10px;
        font-size: 22px;
        cursor: pointer;
    }

    .slider-value-box {
        text-align: center;
        margin-left: 20px;
        margin-top: -15px;
        position: relative;
    }

    .slider {
        width: 80px;
        -webkit-appearance: none;
        appearance: none;
        height: 3px;
        background: lightgray;
        outline: none;
        opacity: 0.7;
        transition: opacity .2s;
        margin-left: 15px;
        margin-top: -15px;
        position: relative;
    }

    .slider:hover {
        opacity: 1;
    }

    .slider::-webkit-slider-thumb {
        -webkit-appearance: none;
        appearance: none;
        width: 14px;
        height: 14px;
        background: white;
        border: 1px solid darkgray;
        cursor: pointer;
        border-radius: 50%;
    }

    .slider::-moz-range-thumb {
        width: 14px;
        height: 14px;
        background: white;
        border: 1px solid darkgray;
        cursor: pointer;
        border-radius: 50%;
    }
</style>
<!--Adin's part(Device) end-->