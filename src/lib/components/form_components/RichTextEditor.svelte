<script>
	// Declare the 'editor' element reference
	/**
	 * @type {HTMLDivElement}
	 */
	let editor;

	export let value = '';
	export let placeholder = 'Start typing here...';

	// Format text with the execCommand function
	// @ts-ignore
	function format(command) {
		// @ts-ignore
		document.execCommand(command, false, null);
	}

	// Update the value when input changes
	// @ts-ignore
	function handleInput(event) {
		value = event.target.innerHTML;
	}
</script>

<!-- Toolbar for formatting options -->
<div class="toolbar">
	<button type="button" on:click={() => format('bold')}>Bold</button>
	<button type="button" on:click={() => format('italic')}>Italic</button>
	<button type="button" on:click={() => format('underline')}>Underline</button>
</div>

<!-- Contenteditable div bound to 'editor' -->
<div
	contenteditable="true"
	class="editor"
	bind:this={editor}
	on:input={handleInput}
	on:focus={() => (editor.innerText === placeholder ? (editor.innerHTML = '') : null)}
	on:blur={() => (editor.innerText === '' ? (editor.innerHTML = placeholder) : null)}
>
	{@html value || placeholder}
</div>

<style>
	.toolbar {
		margin-bottom: 10px;
	}
	button {
		margin-right: 5px;
		padding: 5px 10px;
		font-size: 14px;
		cursor: pointer;
	}
	.editor {
		min-height: 200px;
		border: 1px solid #ccc;
		padding: 10px;
		font-family: Arial, sans-serif;
		font-size: 14px;
		white-space: pre-wrap;
		word-wrap: break-word;
		outline: none;
	}
</style>
