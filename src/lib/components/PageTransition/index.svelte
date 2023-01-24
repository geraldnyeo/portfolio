<script>
    import { fly } from 'svelte/transition';

    export let refresh = '';
</script>

{#key refresh}
    <!-- Issue: If you add an 'out' transition, the text changes first, so the new page transitions out then in again. -->
    <!-- I can't seem to find a solution for this so I'm leaving it for now. -->
    <main
        in:fly="{{ y: 50, duration: 400 }}"
    >
        <br />
        <slot />
    </main>
{/key}

<style>
    main {
        display: flex;
        flex-direction: column;
        flex-grow: 1;
        padding: 50px 100px 50px 50px;
    }

    main br {
        margin-bottom: 100px;
        content: " ";
    }
</style>