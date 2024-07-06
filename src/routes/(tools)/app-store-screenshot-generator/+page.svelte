
<div class="card gap-16 items-center mx-auto max-w-screen-xl lg:grid lg:grid-cols-2 overflow-hidden rounded-lg">
	<!-- Add tool here -->
</div>
<div class="card gap-16 items-center mx-auto max-w-screen-xl lg:grid lg:grid-cols-2 overflow-hidden rounded-lg">
	<!-- Add tool here -->
</div>

<script>
	import { createEventDispatcher } from 'svelte';

	export let background = 'https://static.vecteezy.com/system/resources/previews/011/731/356/non_2x/flat-illustration-of-sea-waves-clouds-and-sun-views-suitable-for-poster-banner-advertising-promotion-and-background-free-vector.jpg';

	let phoneScreens = [
		{ id: 1, background: 'https://thumbs.dreamstime.com/b/d-background-environment-mobile-game-high-quality-vertical-landscape-gaming-template-design-location-generative-ai-275805396.jpg', width: 150, height: 300 },
		{ id: 2, background: 'https://thumbs.dreamstime.com/b/d-background-environment-mobile-game-high-quality-vertical-landscape-gaming-template-design-location-generative-ai-275805396.jpg', width: 150, height: 300 },
		{ id: 3, background: 'https://thumbs.dreamstime.com/b/d-background-environment-mobile-game-high-quality-vertical-landscape-gaming-template-design-location-generative-ai-275805396.jpg', width: 150, height: 300 },
		{ id: 4, background: 'https://thumbs.dreamstime.com/b/d-background-environment-mobile-game-high-quality-vertical-landscape-gaming-template-design-location-generative-ai-275805396.jpg', width: 150, height: 300 },
		{ id: 5, background: 'https://thumbs.dreamstime.com/b/d-background-environment-mobile-game-high-quality-vertical-landscape-gaming-template-design-location-generative-ai-275805396.jpg', width: 150, height: 300 }
	];

	let selectedScreenId = null;

	const dispatch = createEventDispatcher();

	function selectScreen(id) {
		selectedScreenId = id;
		dispatch('select', { id });
	}

	function handleResize(event, screen, direction) {
		event.preventDefault();
		event.stopPropagation();

		const startX = event.clientX;
		const startY = event.clientY;
		const startWidth = screen.width;
		const startHeight = screen.height;

		function onMouseMove(e) {
			const diffX = e.clientX - startX;
			const diffY = e.clientY - startY;

			switch (direction) {
				case 'bottom':
					screen.height = Math.max(startHeight + diffY, 100);
					break;
				case 'top':
					screen.height = Math.max(startHeight - diffY, 100);
					break;
				case 'right':
					screen.width = Math.max(startWidth + diffX, 30);
					break;
				case 'left':
					screen.width = Math.max(startWidth - diffX, 30);
					break;
				default:
					break;
			}

			phoneScreens = [...phoneScreens];
		}

		function onMouseUp() {
			window.removeEventListener('mousemove', onMouseMove);
			window.removeEventListener('mouseup', onMouseUp);
		}

		window.addEventListener('mousemove', onMouseMove);
		window.addEventListener('mouseup', onMouseUp);
	}
</script>

<style>
	.resize-handle {
		position: absolute;
		width: 20px;
		height: 20px;
		background: rgba(0, 0, 0, 0.5);
		border-radius: 50%;
		z-index: 10;
		cursor: pointer;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.resize-handle::after {
		content: '';
		display: block;
		width: 10px;
		height: 10px;
		border-left: 2px solid #fff;
		border-bottom: 2px solid #fff;
		transform: rotate(45deg);
	}

	.bottom {
		bottom: -10px;
		left: calc(50% - 10px);
		cursor: s-resize;
	}

	.top {
		top: -10px;
		left: calc(50% - 10px);
		cursor: n-resize;
	}

	.right {
		top: calc(50% - 10px);
		right: -10px;
		cursor: e-resize;
	}

	.left {
		top: calc(50% - 10px);
		left: -10px;
		cursor: w-resize;
	}

	.screen-container {
		position: relative;
		width: 50px;
		padding-top: calc(100% / 2);
		background-size: cover;
		background-position: center;
		border: 4px solid black;
		border-bottom: 20px solid black;
		border-top: 10px solid black;
		overflow: hidden;
		resize: both;
		min-width: 30px;
		min-height: 50px;
		max-width: 200px;
		gap: 40px;
		max-height: 270px;
	}
</style>

<div class="flex-1 p-4 mb-44 mt-11 v" style="background: url('{background}');">
	<div class="flex justify-between items-start space-x-3">
		{#each phoneScreens as screen}
			<div class="flex flex-col items-center w-1/5">
				<div
					class="relative cursor-pointer rounded-3xl overflow-hidden screen-container {selectedScreenId === screen.id ? 'ring-2 ring-blue-500' : ''}"
					style="width: {screen.width}px; height: {screen.height}px; z-index: {6 - screen.id};"
					on:click={() => selectScreen(screen.id)}
					on:keydown={(e) => { if (e.key === 'Enter' || e.key === ' ') selectScreen(screen.id); }}
					tabindex="0"
					role="button"
					aria-label="Select screen">
					<div class="resize-handle right" on:mousedown={(event) => handleResize(event, screen, 'right')}></div>
					<div class="resize-handle left" on:mousedown={(event) => handleResize(event, screen, 'left')}></div>
					<div class="absolute inset-0" style="background: url('{screen.background}') no-repeat center / cover;"></div>
				</div>
			</div>
		{/each}
	</div>
</div>
