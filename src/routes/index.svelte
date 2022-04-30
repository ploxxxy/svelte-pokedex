<script context="module">
    export async function load() {
        const res = await fetch('https://pokeapi.co/api/v2/pokemon?limit=386').then(r => r.json())
        const pokemon = res.results.map((data, index) => {
                return {
                    name: data.name,
                    id: index + 1,
                    image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index + 1}.png`
                }
            })

    return { props: { pokemon:pokemon } }
    
    }
</script>

<script>
    import Card from "../components/card.svelte"
    export let pokemon
    let searchTerm = ""
    let filteredPokemon = []

    $: {
        if (searchTerm) {
            filteredPokemon = pokemon.filter(pokemon => pokemon.name.toLowerCase().includes(searchTerm.toLowerCase()))
        } else {
            filteredPokemon = [...pokemon]
        }
    }
</script>

<svelte:head>
    <title>Svelte Kit Pokedex</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase">Svelte Kit Pokedex</h1>

<input class="w-full rounded-md text-lg p-4 my-6 border-2 border-gray-200" bind:value="{searchTerm}" type="text" placeholder="Search Pokedex">

<div class="grid gap-4 xl:grid-cols-4 md:grid-cols-2 grid-cols-1">
    {#each filteredPokemon as pokemon}
    <Card pokemon={pokemon} />
    {/each}
</div>