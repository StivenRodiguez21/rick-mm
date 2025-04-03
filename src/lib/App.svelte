<script>
  import Cards from "../lib/Cards.svelte"; // Importamos el componente Cards
  let caracteres = [];
  let pagina = 1;

  async function loadCharacters() {
    const response = await fetch(
      `https://rickandmortyapi.com/api/character?page=${pagina}`,
    );
    const data = await response.json();
    console.log(data);
    caracteres = data.results;
  }

  function siguiente() {
    pagina++;
    loadCharacters();
  }

  function anterior() {
    if (pagina > 1) {
      pagina--;
      loadCharacters();
    }
  }

  loadCharacters();
</script>

<h1 class="title">Rick and Morty Svelte</h1>
<h2 class="title">Página: {pagina}</h2>

<div class="contenedor">
  <div class="botones">
    <button class="boton" on:click={anterior} disabled={pagina === 1}
      >Anterior</button
    >
    <button class="boton" on:click={siguiente}>Siguiente</button>
  </div>

  {#if caracteres.length === 0}
    <p>Cargando personajes...</p>
  {:else}
    {#each caracteres as personaje}
      <Cards caracter={personaje} />
    {/each}
  {/if}
</div>
