<script>
    import { cubicInOut } from 'svelte/easing';
    import projects from '../../lib/data/projects.json';

    let card = '';
    let select = '';

    // Transitions
    const t_screen_in = (node, { duration = 1000 }) => {
        const maxHeight = node.parentNode.clientHeight;

        return {
            duration,
            easing: cubicInOut,
            tick: t => {
                let height = t * maxHeight
                node.style.height = `${height}px`;
            }
        }
    }
</script>

<h1>projects</h1>

<br /> <br />
<p>
    I love building coding projects - I believe it's the best way to learn new skills and put fresh knowledge to practice.
    This page showcases a few of the personal projects which I am most proud of. 
    You can find a more complete list of projects I have worked on, on my <a href="https://github.com/geraldnyeo">GitHub</a>.
    Feel free to contact me if you want to collaborate on any interesting projects!
</p>

<br /> <hr />

<div id="projects-wrapper">
    {#each projects as project}
        <div class="project" 
            on:mouseenter={() => {
                card = project.name;
            }}
            on:mouseleave={() => {
                card = '';
                select = '';
            }}
            on:mousedown={() => {
                select = project.name;
            }}
            on:mouseup={() => {
                select = '';
            }}>
            <img src={`/images/${project.img}`} alt={`${project.name}'s icon`}/>
            <br />
            <span>{project.name}</span>
            
            <div class="links">
                {#if card === project.name}
                    {#each project.links as link (link[0])}
                        <a href={link[1]}
                            target="_blank"
                            rel="noopener noreferrer"
                            on:mousedown|stopPropagation
                            >
                            {link[0]}
                        </a>
                    {/each}
                {/if}
            </div>
            
            {#if select === project.name}
                <div class="description" transition:t_screen_in>
                    <p>{project.description}</p>
                </div>
            {/if}
        </div>
    {/each}
</div>

<style>
    h1 {
        font-size: 64px;
    }

    hr {
        border-top: 1px solid black;
        margin: 20px;
    }

    #projects-wrapper {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
        grid-gap: 40px;
        margin: 20px;
    }

    .project {
        display: flex;
        flex-direction: column;
        align-items: center;
        position: relative;
        height: 250px;
        background-color: #fafafa;
        box-shadow: 2px 2px #aaaaaa;
        overflow: hidden;
    }

    .project img {
        display: block;
        margin-top: 10%;
        max-width: 50%;
        max-height: 50%;
        width: auto;
        height: auto;
    }

    .project span {
        padding: 10px;
    }

    .project .links {
        display: flex;
        flex-direction: row;
    }

    .project .links a {
        margin-left: 3px;
        margin-right: 3px;
        padding: 1px;
    }

    .project .description {
        position: absolute;
        width: 100%;
        margin-bottom: auto;
        overflow: hidden;
        background-color: #f3f3f3;
    }

    .project .description p {
        padding: 20px 24px;
        margin-bottom: auto;
        word-break: break-word;
    }
</style>