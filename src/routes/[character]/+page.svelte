<script>
    import { page } from '$app/stores'

    const getCharacter = async () => {
        const res = await fetch(`https://potterapi-fedeperin.vercel.app/en/characters?index=${ $page.params.character }`)
        const data = await res.json()

        return data
    }
</script>

<a href="../">Go Back</a>

{#await getCharacter()}
    Loading Character Data
{:then { image, fullName, nickname, hogwartsHouse, children, interpretedBy }}
    <section>
        <img src={ image } alt={ fullName }>
        <div class="data">
            <h1>{ fullName }</h1>
            <p>Nickname: { nickname }</p>
            <p>House: { hogwartsHouse }</p>
            {#if children[0]}
                <p>
                    Children: 
                    {#each children as child, index}
                        { child }{ 
                            (index == children.length - 2) ? 
                            ' and ' : 
                            (index != children.length - 1) ? ', ' : '' 
                        }
                    {/each}
                </p>
            {/if}
            <p>Interpreted by:  { interpretedBy }</p>
        </div>
    </section>
{:catch error}
    Error getting the character data { error }
{/await}


<style>
    a {
        text-decoration: none;
        font-size: 18px;
        margin-bottom: 10px;
        display: flex;
        color: inherit;
        font-weight: lighter;
        padding: 15px;
        border: 1px solid currentColor;
        width: 130px;
        justify-content: center;
        transition: opacity .2s ease;
    }

    a:hover {
        opacity: .8;
    }

    section {
        display: flex;
    }

    h1 {
        margin-bottom: 5px;
    }

    img {
        margin-right: 20px;
    }

    @media (max-width: 800px) {
        section {
            flex-direction: column;
        }

        img {
            width: 100%;
            margin-bottom: 20px;
        }
    }
</style>