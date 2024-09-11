<script>
    import { fade, fly } from 'svelte/transition';
    import { page } from '$app/stores';
    import PageTransition from "../lib/components/PageTransition/index.svelte";

    let refresh = '';
    $: refresh = $page.route.id;
</script>

<aside>
    <div id="navline">
        <ul>
            <li><a href="/">home</a></li>
            <li><a href="/about">about</a></li>
            <li><a href="/projects">projects</a></li>
        </ul>
    </div>
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
        padding: 0 30px 0 30px;
    }

    aside li {
        position: relative;
        left: -25px;
        list-style: none;
        background-image: url("images/nav_bullet.png");
        background-repeat: no-repeat;
        background-size: 10px;
        background-position: 0 .25em;
        padding-left: 1.2em;
    }

    aside a {
        margin: 2px 0 2px 0;
        color: black;
        text-decoration: none;
    }

    #navline {
        display: flex;
        flex-direction: column;
        justify-content: center;
        flex: 1;
        padding: 0 20px 0 20px;
        border-left: 2px solid #e0bfb7;
        background: transparent;
    }

    #main-wrapper {
        display: flex;
        flex-direction: column;
        flex: 1;
    }

    footer {
        display: flex;
        align-self: end;
        padding: 0 100px 30px 0;
    }
</style>