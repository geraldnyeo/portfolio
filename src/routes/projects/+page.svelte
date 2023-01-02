<script>    
    import projects from '../../lib/data/projects.json';

    let card = '';
    let select = '';
</script>

<h1>projects</h1>

<br />
<p>
    Mauris eget consectetur lectus, et pretium lectus. Pellentesque sollicitudin arcu ut nulla pretium, non accumsan nulla posuere.
    Ut lacus quam, consequat eu accumsan ut, eleifend a dui. Phasellus imperdiet, tortor nec dictum convallis, magna massa mollis
    ipsum, ut elementum elit ipsum eu sapien. Aliquam erat volutpat. Vestibulum consequat ultrices velit vitae auctor. 
    Pellentesque feugiat tortor ut ex euismod scelerisque. Sed quis lorem id velit malesuada mollis. Aliquam erat volutpat. 
    Aliquam eu porta metus. Fusce interdum tristique ullamcorper.
</p>

<hr />

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
            {#if select === ''}
                <img src={`/images/${project.img}`} alt={`${project.name}'s icon`}/>
                <br />
                <span>{project.name}</span>
                
                {#if card === project.name}
                    {#each project.links as link (project.id)}
                        <!-- TODO: Link no longer works because click clicks the div -->
                        <!-- There's a solution to this on the svelte tutorial -->

                        <a href={link[1]}
                            target="_blank"
                            rel="noopener noreferrer"
                            >
                            {link[0]}
                        </a>
                    {/each}
                {/if}
            {/if}

            {#if select === project.name}
                <p>{project.description}</p>
            {/if}
        </div>
    {/each}

    <div class="project">
    </div>
    <div class="project">
    </div>
    <div class="project">
    </div>
    <div class="project">
    </div>
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
    }

    .project {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 250px;
        margin: 20px;
        padding: 10px;
        background-color: #fafafa;
        box-shadow: 2px 2px #aaaaaa;
    }

    .project img {
        display: block;
        max-width: 50%;
        max-height: 50%;
        width: auto;
        height: auto;
    }

    .project span {
        padding: 10px;
    }

    .project p {
        padding: 20px 12px;
        margin-bottom: auto;
    }
</style>