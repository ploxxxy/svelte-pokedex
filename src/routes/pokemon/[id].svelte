<script context="module">
    export async function load({ params }) {
        const pokemon = await fetch(`https://pokeapi.co/api/v2/pokemon/${params.id}`).then(r => r.json())
        return {
            props: { pokemon }
        }
    }
</script>

<script>
    export let pokemon
</script>

<div class="flex flex-col items-center bg-gray-100 my-4 rounded-xl shadow-md">

    <h1 class="text-4xl text-center my-8 uppercase">{pokemon.name}</h1>
    <p class="uppercase">
        Type: <strong>{pokemon.types[0].type.name}</strong> | Height: <strong>{pokemon.height}</strong>
        | Weight: <strong>{pokemon.weight}</strong>
    </p>

    <div class="flex flex-row items-center my-8">
        <img src="{pokemon.sprites['front_default']}" alt="{pokemon.name} Default" class="card-image h-40 w-40">
        <img src="{pokemon.sprites['front_shiny']}" alt="{pokemon.name} Shiny" class="card-image h-40 w-40">
    </div>

    <div class="grid gap-4 xl:grid-cols-6 md:grid-cols-2 grid-cols-1 my-8">
        {#each pokemon.stats as stat}
            <div class="p-2 bg-gray-200 text-gray-800 text-center rounded-md shadow-sm flex flex-col items-center">
                <h2 class="uppercase text-sm">{stat.stat.name}: {stat.base_stat}</h2>
            </div>
        {/each}
</div>
    
</div>

<h1 class="text-2xl text-center uppercase my-4">moves:</h1>
<div class="grid gap-4 xl:grid-cols-6 md:grid-cols-4 grid-cols-2">
        {#each pokemon.moves as move}
            <div class="p-2 bg-gray-100 text-gray-800 text-center rounded-md shadow-sm flex flex-col items-center">
                <h2 class="uppercase text-sm">{move.move.name}</h2>
            </div>
        {/each}
</div>