<script>
    import { fly, fade } from 'svelte/transition';

    export let name = "";
    export let phone = "";

    $: message = "";
    $: stage = 0;

    function nameHandler() {
        if(name === "") {
            message = "Sorry, you need to insert something here";
        } else {
            message = "";
            stage += 1;
        }
    }
</script>

<main>
<!--     <header>
        <h1>Hey there!</h1>
        <p>Since this is not the real WhatsApp, could you inform us some number (it can be a fake one) and a user name?</p>
        <p>It's just for us to have something to display on the UI</p>
    </header> -->
        {#if stage === 0}
            <div class="login-card">
                <p>Your name is...</p>
                <input type="text" required placeholder="name" bind:value={name}>
                <div class="button-aligner">
                    <button on:click={nameHandler}>next!</button>
                </div>
                <div class="message-box">
                    {message}
                </div>
            </div>
        {:else if stage === 1 }
            <div class="login-card" in:fly={{x: 400, duration: 500}} out:fade>
                <p>Hello {name}, insert a phone: </p>
                <input type="text" required placeholder="A fake should do" bind:value={phone}>
                <div class="button-aligner">
                    <button on:click={() => {stage += 1}}>Done!</button>
                </div>
                <div class="message-box">
                    {message}
                </div>
            </div>
        {/if}
</main>

<style>
    main {
        background-color: #090E11;
        width: 100vw;
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        overflow: hidden;
    }

    p {
        color: #D8D9DB;
    }

    .login-card {
        background-color:  #262D31;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 60vh;
        width: 40vw;
        padding: 20px;
        border-radius: 5px;
    }

    input {
        margin-top: 20px;
        padding: 3px;
        background-color: inherit;
        border: 1px solid #117b70;
        color: #12d6c3;
        height: 30px;
    }

    .button-aligner {
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: flex-end;
        padding-top: 10px;
    }

    button {
        width: 40px;
        height: 40px;
        background-color: #117B70;
        color: #fff;
        border-radius: 10px;
        border: none;
        outline: none;
    }

    button:focus {
        border: none;
        outline: none;
    }

    .message-box {
        color: #117B70;
        font-size: 15px;
    }
</style>