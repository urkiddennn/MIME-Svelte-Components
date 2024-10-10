<script>
    export let value = ""; // Bound value for the password
    export let placeholder = "Enter your password"; // Placeholder text
    export let minLength = 6; // Minimum length for validation
    export let isValid = true; // Validation state
 
    // Show/Hide password visibility toggle
    let showPassword = false;
 
    // Check password validity based on minimum length
    $: isValid = value.length >= minLength;
 
    // Handle input event
    function handleInput(event) {
       value = event.target.value;
    }
 </script>
 
 <div class="password-input">
    <input
       type={showPassword ? 'text' : 'password'} <!-- Keep type dynamic based on visibility -->
       bind:value={value} <!-- Bind value as usual -->
       placeholder={placeholder}
       on:input={handleInput}
       class:invalid={!isValid}
    />
    <button type="button" class="toggle" on:click={() => (showPassword = !showPassword)}>
       {showPassword ? "Hide" : "Show"}
    </button>
    {#if !isValid}
       <span class="error">Password must be at least {minLength} characters.</span>
    {/if}
 </div>
 
 <style>
    .password-input {
       position: relative;
       margin-bottom: 10px;
    }
 
    input {
       width: 100%;
       padding: 10px;
       border: 1px solid #ccc;
       border-radius: 4px;
    }
 
    input.invalid {
       border-color: red;
    }
 
    .toggle {
       position: absolute;
       right: 10px;
       top: 50%;
       transform: translateY(-50%);
       background: transparent;
       border: none;
       cursor: pointer;
       color: #007bff;
    }
 
    .error {
       color: red;
       font-size: 0.8em;
       margin-top: 5px;
    }
 </style>
 