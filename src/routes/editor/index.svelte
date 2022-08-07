<script lang="ts">
  import storage from "$lib/services/storage";

  const textures = storage.get<Array<{ name: string; url: string }>>(
    "textures",
    []
  );
  let name = "naamloos";
  let disabled = true;
  let value = "";

  function onAdd() {
    textures.push({ name, url: value });
    storage.set("textures", textures);
  }
</script>

<div style:padding="10px">
  <h3>Afbeeldingen</h3>
  <ul>
    {#each textures as texture, index}
      <li>
        <a href="/editor/tiles/{index}">
          <img
            src={texture.url}
            width="auto"
            height="32"
            alt=" {index}"
          />{texture.name}
        </a>
      </li>
    {/each}
  </ul>
  <h3>Afbeelding toevoegen</h3>
  <label>
    Naam
    <input type="text" bind:value={name} />
  </label>
  <textarea name="" id="" bind:value />
  <button on:click={onAdd} {disabled}>Toevoegen</button>
  <div class="preview">
    <img
      src={value}
      alt="preview"
      on:error={() => {
        disabled = true;
      }}
      on:load={() => {
        disabled = false;
      }}
    />
  </div>
</div>

<style>
  textarea {
    display: block;
    width: 100%;
    box-sizing: border-box;
  }
  .preview {
    display: inline-block;
    padding: 5px;
    background-color: #626262;
  }
</style>
