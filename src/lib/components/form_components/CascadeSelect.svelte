<script>
	export let values = {}; // Pass values as a prop

	let selectedCountry = '';
	let selectedState = '';
	let selectedCity = '';

	// Get states based on selected country
	let states = [];
	// @ts-ignore
	$: states = selectedCountry ? Object.keys(values[selectedCountry]) : [];

	// Get cities based on selected state
	let cities = [];
	// @ts-ignore
	$: cities = selectedState ? values[selectedCountry][selectedState] : [];

	// Reset state and city when the country changes
	function onCountryChange() {
		selectedState = '';
		selectedCity = '';
	}

	// Reset city when the state changes
	function onStateChange() {
		selectedCity = '';
	}
</script>

<div class="cascade-select">
	<!-- Country Select -->
	<label for="country">Country</label>
	<select id="country" bind:value={selectedCountry} on:change={onCountryChange}>
		<option value="">Select a country</option>
		{#each Object.keys(values) as country}
			<option value={country}>{country}</option>
		{/each}
	</select>

	<!-- State/Province Select -->
	<label for="state">State/Province</label>
	<select
		id="state"
		bind:value={selectedState}
		on:change={onStateChange}
		disabled={!selectedCountry}
	>
		<option value="">Select a state/province</option>
		{#each states as state}
			<option value={state}>{state}</option>
		{/each}
	</select>

	<!-- City Select -->
	<label for="city">City</label>
	<select id="city" bind:value={selectedCity} disabled={!selectedState}>
		<option value="">Select a city</option>
		{#each cities as city}
			<option value={city}>{city}</option>
		{/each}
	</select>

	<!-- Display selected values -->
	<div class="selections">
		<p>Selected Country: {selectedCountry}</p>
		<p>Selected State/Province: {selectedState}</p>
		<p>Selected City: {selectedCity}</p>
	</div>
</div>

<style>
	.cascade-select {
		display: flex;
		flex-direction: column;
		gap: 10px;
		max-width: 300px;
		margin: 20px auto;
	}
	label {
		font-weight: bold;
		margin-bottom: 5px;
	}
	select {
		padding: 5px;
		font-size: 14px;
	}
</style>
