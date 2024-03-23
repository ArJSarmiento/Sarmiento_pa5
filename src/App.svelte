<script lang="ts">
  interface Pokemon {
    name: string;
    url: string;
    height: number;
    weight: number;
    order: number;
    base_experience: number;
  }
  let pokemons: Pokemon[] = [];

  async function fetchData(): Promise<void> {
    const response = await fetch("https://pokeapi.co/api/v2/pokemon?limit=10");
    const data = await response.json();
    for (const pokemon of data.results) {
      const response = await fetch(pokemon.url);
      const data = await response.json();
      pokemon.height = data.height;
      pokemon.weight = data.weight;
      pokemon.order = data.order;
      pokemon.base_experience = data.base_experience;
    }
    pokemons = data.results;
  }

  fetchData();
</script>

<svelte:head>
  <title>Prog Assignment 1. Web API Data</title>
</svelte:head>

<main>
  <div id="data-container">
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Base Experience</th>
          <th>Height</th>
          <th>Weight</th>
          <th>Order</th>
          <th>Details URL</th>
        </tr>
      </thead>
      <tbody>
        {#each pokemons as { name, url, height, weight, order, base_experience }}
          <tr>
            <td>{name}</td>
            <td>{base_experience}</td>
            <td>{height}</td>
            <td>{weight}</td>
            <td>{order}</td>
            <td><a href={url}>Info</a></td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
</main>

<style>
  table {
    width: 100%;
    border-collapse: collapse;
  }

  td {
    padding: 10px;
    border: 1px solid black;
  }

  #data-container {
    width: 100%;
  }
</style>
