<script>
	// @ts-ignore
	import CascadeSelect from './components/form_components/CascadeSelect.svelte';
	// @ts-ignore
	import IconField from './components/form_components/IconField.svelte';
	// @ts-ignore
	import InputOtp from './components/form_components/InputOTP.svelte';
	// @ts-ignore
	import Knob from './components/form_components/Knob.svelte';
	import ListBox from './components/form_components/ListBox.svelte';
	import PasswordInput from './components/form_components/PasswordInput.svelte';
	// @ts-ignore
	import RichTextEditor from './components/form_components/RichTextEditor.svelte';

	let password = '';
</script>

<h2>Create a Password:</h2>
<PasswordInput bind:value={password} minLength={8} />
<p>Your password: {password}</p>
