<script>
    import CharacterCard from '$components/CharacterCard.svelte'

    const fetchCharacters = async () => {
        const res = await fetch('https://potterapi-fedeperin.vercel.app/en/characters')
        const data = await res.json()

        return data
    }
</script>

{#await fetchCharacters()}
    <p>Loading Characters...</p>
{:then characters}
    <section class="characters">
        {#each characters as character}
            <CharacterCard { character } />
        {/each}
    </section>
{:catch error}
    <p>Error loading the characters { error }</p>
{/await}

<style>
    section {
        display: grid;
        grid-template-columns: repeat(6, 1fr);
        width: 100%;
        grid-gap: 20px;
    }

    @media(max-width: 1500px) {
        section {
            grid-template-columns: repeat(4, 1fr);
        }
    }

    @media(max-width: 850px) {
        section {
            grid-template-columns: repeat(3, 1fr);
        }
    }

    @media(max-width: 650px) {
        section {
            grid-template-columns: repeat(2, 1fr);
        }
    }

    @media(max-width: 450px) {
        section {
            grid-template-columns: 1fr;
        }
    }
</style>