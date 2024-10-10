<script>
	export let length = 6; // Default OTP length (can be changed)
	export let otp = ''; // Bound OTP value
	let inputs = new Array(length).fill(''); // Array to hold the individual input values

	// Handle input changes and focus management
	// @ts-ignore
	function handleInput(event, index) {
		const value = event.target.value;
		if (!/^\d$/.test(value)) return; // Only allow a single digit

		inputs[index] = value;
		otp = inputs.join(''); // Update the OTP value with all digits

		// Focus on the next input if available
		const nextInput = document.querySelector(`#otp-${index + 1}`);
		if (nextInput) {
			// @ts-ignore
			nextInput.focus();
		}
	}

	// Handle key down for backspace
	// @ts-ignore
	function handleKeyDown(event, index) {
		if (event.key === 'Backspace' && inputs[index] === '') {
			const previousInput = document.querySelector(`#otp-${index - 1}`);
			if (previousInput) {
				// @ts-ignore
				previousInput.focus();
			}
		}
	}
</script>

<div class="otp-container">
	{#each inputs as _, i}
		<input
			id={'otp-' + i}
			type="text"
			class="otp-input"
			maxlength="1"
			bind:value={inputs[i]}
			on:input={(e) => handleInput(e, i)}
			on:keydown={(e) => handleKeyDown(e, i)}
			inputmode="numeric"
		/>
	{/each}
</div>

<style>
	.otp-container {
		display: flex;
		gap: 10px;
	}
	.otp-input {
		width: 40px;
		height: 40px;
		text-align: center;
		font-size: 24px;
		border: 1px solid #ccc;
		border-radius: 4px;
		outline: none;
	}
	.otp-input:focus {
		border-color: #007bff;
		box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
	}
</style>
