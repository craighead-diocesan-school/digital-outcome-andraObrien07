<script>
    import Header from "$lib/Header.svelte";
    import { login } from "$lib/db.js";
    import { goto } from "$app/navigation";
    import { onMount } from "svelte";
    import { user } from "$lib/state.svelte.js";

    onMount(() => {
        if (localStorage.getItem("user") && !user.uid) {
            let data = JSON.parse(localStorage.getItem("user"));
            console.log("Loading user from localStorage:", data);
            user.uid = data.uid;
            user.email = data.email;
            user.displayName = data.displayName;
            user.photoURL = data.photoURL;
            console.log("User loaded from localStorage:", user);
            // getCharacter(data.uid);
        }
    });
</script>

<Header />

<main>
    <button
        class="button"
        on:click={() => {
            login();
            goto("/farms");
        }}
    >
        login
    </button>
    <button
        class="button"
        on:click={() => {
            login();
            goto("/farms");
        }}
    >
        Sign In
    </button>

    <h2>
        <p>Take your land from Patch to Plenty with Green Patch</p>
    </h2>

    <a href="/acts"
        ><img class="logo" src="/ChatGPTimage.png" alt="GreenPatch Logo" /></a
    >
</main>
