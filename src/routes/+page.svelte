<script>
    import Header from "$lib/Header.svelte";
    import { login } from "$lib/db.js";
    import { goto } from "$app/navigation";
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
</main>
