<script>
    import { fade, fly } from 'svelte/transition';
    import { page } from '$app/stores';
    import PageTransition from "../lib/components/PageTransition/index.svelte";

    let refresh = '';
    $: refresh = $page.route.id;
</script>

<aside>
    <a href="/">home</a>
    <a href="/about">about</a>
    <a href="/projects">projects</a>
</aside>


<div id="main-wrapper">
    {#key refresh}
        <PageTransition>
            <slot />
        </PageTransition>
    {/key}

    <footer>
        2023
    </footer>
</div>


<style>
    /* CSS Reset */
    :global(*) {
        margin: 0;
        padding: 0;
        border: 0;
        outline: 0;
        color: black;
        font-size: 100%;
        vertical-align: baseline;
        background: transparent;
    }

    :global(html, body) {
        height: 100%;
    }

    :global(body) {
        display: flex;
        background-image: url("/images/bg.jpg");
        background-size: cover;
    }

    aside {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 0 50px 0 50px;
        background: transparent;
    }

    aside a {
        text-decoration: none;
    }

    #main-wrapper {
        display: flex;
        flex-direction: column;
    }

    footer {
        display: flex;
        align-self: end;
        padding: 0 100px 30px 0;
    }
</style>