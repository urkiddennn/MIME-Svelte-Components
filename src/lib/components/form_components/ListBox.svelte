<script>
	// @ts-ignore
	/**
	 * @type {any[]}
	 */
	export let options = []; // List of options with grouping
	// @ts-ignore
	/**
	 * @type {any[]}
	 */
	export let selected = []; // Currently selected options

	// Toggle selection of an option
	// @ts-ignore
	function toggleOption(option) {
		// @ts-ignore
		if (selected.includes(option)) {
			// @ts-ignore
			selected = selected.filter((item) => item !== option);
		} else {
			// @ts-ignore
			selected = [...selected, option];
		}
	}
</script>

<div class="listbox">
	{#each options as { group, items }}
		<div class="group">
			<div class="group-title">{group}</div>
			{#each items as option}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<!-- svelte-ignore a11y-no-static-element-interactions -->
				<div class="option" on:click={() => toggleOption(option)}>
					<input type="checkbox" checked={selected.includes(option)} readOnly />
					<span>{option}</span>
				</div>
			{/each}
		</div>
	{/each}
</div>

<style>
	.listbox {
		max-height: 200px; /* Adjust the height as needed */
		overflow-y: auto;
		border: 1px solid #ccc;
		border-radius: 5px;
		padding: 10px;
		background: white;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
	}

	.group {
		margin-bottom: 10px;
	}

	.group-title {
		font-weight: bold;
		margin-bottom: 5px;
		color: #333;
	}

	.option {
		display: flex;
		align-items: center;
		padding: 5px;
		cursor: pointer;
		transition: background 0.2s;
	}

	.option:hover {
		background-color: #f0f0f0;
	}

	input[type='checkbox'] {
		margin-right: 10px;
	}
</style>
