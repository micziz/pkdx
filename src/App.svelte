<script lang="ts">
  import { PokemonClient } from 'pokenode-ts';
  import capitalize from 'just-capitalize';

  const api = new PokemonClient();
  let data;
  let sprite;
  let abilites;
  let name;
  let moves;
  let types;
  let height;
  let weight;
  let exp;
  let id;
  

  async function onSubmit(){
    await api
        .getPokemonByName(data)
        .then((data) => {
          name = data.name
          sprite = data.sprites.front_default
          abilites = data.abilities
          moves = data.moves;
          types = data.types
          height = data.height;
          weight = data.weight;
          exp = data.base_experience;
          id = data.id;
        }) // will output "Luxray"
        .catch((error) => console.log(error));
  }

</script>

<main>
  <h1>PKDX</h1>

  <form on:submit|preventDefault={onSubmit}>
    <div id="input">
      <input type="text" bind:value={data} name="" id="">
    </div>
    <div id="sub">
      <button type="submit">Search</button>
    </div>
  </form>

  {#if sprite != undefined}
    <h2>{capitalize(name)}</h2>
    <img src={sprite} height="200" width="200" alt="pokemon main sprite">
    
    <p> <strong>Id: {id}</strong> </p>
    <p> <strong>Height: {height}cm</strong> </p>
    <p> <strong>Weight: {weight}g</strong> </p>
    <p> <strong>Base Exp: {exp}</strong> </p>
    <p> <strong>Types</strong> </p>
    {#each types as type}
      <p>{type.type.name}</p>
    {/each}
    <p> <strong>Abilities</strong> </p>
    {#each abilites as ability}
    <p>{ability.ability.name}</p>
    {/each}
    <p> <strong>Moves</strong> </p>
    {#each moves as move}
      <p>{move.move.name}</p>
    {/each}
  {:else}
    <h1>No pokemon inserted.</h1>
  {/if}
</main>

<style>

  #input{
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  #sub{
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 20px;
  }
</style>