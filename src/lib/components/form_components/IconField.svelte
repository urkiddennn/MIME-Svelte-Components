<script>
	// @ts-nocheck

	export let icon = ''; // Icon HTML or text
	export let placeholder = 'Enter text...'; // Placeholder text
	export let value = ''; // Input value bound to the parent
	export let type = 'text'; // Input type (text, password, etc.)

	/**
	 * @param {{ target: { value: string; }; }} event
	 */
	function handleInput(event) {
		value = event.target.value;
	}
</script>

<div class="icon-field">
	<span class="icon" aria-hidden="true">
		{@html icon}
		<!-- Render the icon (could be HTML or text) -->
	</span>
	{#if type === 'text'}
		<input type="text" bind:value {placeholder} on:input={handleInput} />
	{:else if type === 'password'}
		<input type="password" bind:value {placeholder} on:input={handleInput} />
	{:else if type === 'email'}
		<input type="email" bind:value {placeholder} on:input={handleInput} />
	{/if}
</div>

<style>
	.icon-field {
		display: flex;
		align-items: center;
		border: 1px solid #ccc;
		border-radius: 5px;
		padding: 5px 10px;
		max-width: 300px;
	}
	.icon {
		margin-right: 10px;
		font-size: 1.2em;
	}
	input {
		border: none;
		outline: none;
		font-size: 16px;
		flex: 1;
	}
	input::placeholder {
		color: #888;
	}
</style>
