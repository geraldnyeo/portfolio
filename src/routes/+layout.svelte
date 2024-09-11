<script>
    import { fade, fly } from 'svelte/transition';
    import { page } from '$app/stores';
    import PageTransition from "../lib/components/PageTransition/index.svelte";

    let refresh = '';
    $: refresh = $page.route.id;

    let dropdown = false;
</script>

<aside id="nav-lg">
    <div id="navline">
        <ul>
            <li><a href="/">home</a></li>
            <li><a href="/about">about</a></li>
            <li><a href="/projects">projects</a></li>
        </ul>
    </div>
</aside>


<div id="nav-sm">
    <div id="navblock">
        <div id="dropdown-btn"
            on:mousedown={() => {
                dropdown = !dropdown;
            }}>
            <img src="/images/nav_bullet.png" />
            <img src="/images/nav_bullet.png" />
            <img src="/images/nav_bullet.png" />
        </div>
        {#if dropdown}
            <ul id="dropdown">
                <li><a href="/">home</a></li>
                <li><a href="/about">about</a></li>
                <li><a href="/projects">projects</a></li>
            </ul>
        {/if}
    </div>
</div>


<div id="main-wrapper">
    {#key refresh}
        <PageTransition>
            <slot />
        </PageTransition>
    {/key}

    <footer>
        2024
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

    /*Responsive Navbar*/
    @media only screen and (max-width: 600px) {
        #nav-lg {
            display: none;
        }

        #nav-sm {
            display: flex;
        }
    }

    @media only screen and (min-width: 600px) {
        #nav-lg {
            display: flex;
            padding: 0 30px 0 30px;
        }

        #nav-sm {
            display: none;
        }
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

    #navline li {
        position: relative;
        left: -25px;
        list-style: none;
        background-image: url("images/nav_bullet.png");
        background-repeat: no-repeat;
        background-size: 10px;
        background-position: 0 .25em;
        padding-left: 1.2em;
    }

    #navline a {
        margin: 2px 0 2px 0;
        color: black;
        text-decoration: none;
    }

    #nav-sm {
        position: fixed;
        width: 100%;
        top: 0;
        overflow: hidden;
        z-index: 99;
    }

    #navblock {
        display: flex;
        flex-direction: column;
        flex-basis: 100%;
        background: #e0bfb7;
    }

    #dropdown-btn {
        display: flex;
        flex-direction: row;
        justify-content: center;
        padding: 10px;
    }

    #dropdown {
        display: flex;
        flex-direction: column;
    }

    #navblock li {
        list-style: none;
        padding: 10px;
        text-align: center;
    }

    #navblock a {
        margin: 2px 0 2px 0;
        color: black;
        text-decoration: none;
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