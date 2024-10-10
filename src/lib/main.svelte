<script>
	import CascadeSelect from './components/form_components/CascadeSelect.svelte';
	import IconField from './components/form_components/IconField.svelte';
	import InputOtp from './components/form_components/InputOTP.svelte';
	import RichTextEditor from './components/form_components/RichTextEditor.svelte';

	let otpValue = '';
</script>

<h1>Hello Home</h1>

<InputOtp bind:otp={otpValue} length={6} />
