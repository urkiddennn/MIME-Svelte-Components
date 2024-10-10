<script>
	export let min = 0; // Minimum value
	export let max = 100; // Maximum value
	export let value = 50; // Current value, bound to parent component

	// Calculate the rotation based on the current value
	$: rotation = ((value - min) / (max - min)) * 360;

	// Handle mouse events for adjusting the knob
	let isDragging = false;

	// @ts-ignore
	function handleMouseDown(event) {
		isDragging = true;
		window.addEventListener('mousemove', handleMouseMove);
		window.addEventListener('mouseup', handleMouseUp);
	}

	// @ts-ignore
	function handleMouseMove(event) {
		if (!isDragging) return;
		const rect = event.target.getBoundingClientRect();
		const centerX = rect.left + rect.width / 2;
		const centerY = rect.top + rect.height / 2;

		const angle = Math.atan2(event.clientY - centerY, event.clientX - centerX) * (180 / Math.PI);
		const normalizedAngle = (angle + 180 + 360) % 360; // Normalize to 0-360
		const percentage = normalizedAngle / 360;

		value = Math.round(min + percentage * (max - min));
		value = Math.max(min, Math.min(max, value)); // Ensure within bounds
	}

	function handleMouseUp() {
		isDragging = false;
		window.removeEventListener('mousemove', handleMouseMove);
		window.removeEventListener('mouseup', handleMouseUp);
	}
</script>

<div class="knob" on:mousedown={handleMouseDown}>
	<div class="knob-inner" style="transform: rotate({rotation}deg);"></div>
	<div class="value">{value}</div>
</div>

<style>
	.knob {
		position: relative;
		width: 100px;
		height: 100px;
		border: 8px solid #ccc;
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
		cursor: pointer;
		user-select: none; /* Prevent text selection */
	}

	.knob-inner {
		position: absolute;
		width: 100%;
		height: 100%;
		border-radius: 50%;
		background: conic-gradient(#007bff, #007bff 50%, #e9ecef 50%);
	}

	.value {
		position: absolute;
		font-size: 1.2em;
		color: #333;
	}
</style>
