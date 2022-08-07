<script lang="ts">
  import { Rectangle, Texture } from "pixi.js";
  import { Container, Sprite } from "svelte-pixi";
  import EditorPanel from "$lib/components/EditorPanel.svelte";
  import Engine from "$lib/components/Engine.svelte";
  import Control from "$lib/components/Control.svelte";
  import storage from "$lib/services/storage";
  // eslint-disable-next-line import/extensions
  import { page } from "$app/stores";

  const data = storage.get("textures", [])[$page.params.index];
  let name = "";
  let x = 0;
  let y = 0;
  let width = 0;
  let height = 0;

  let texture: Texture | undefined;
  let framed: Texture | undefined;
  $: {
    x;
    y;
    width;
    height;
    update();
  }

  function onLoad(result: Texture) {
    texture = result;
    width = result.height;
    height = result.height;
    framed = new Texture(result.baseTexture);
  }
  Texture.fromURL(data.url).then(onLoad);

  function update() {
    if (texture && framed) {
      const clampedX = Math.max(0, Math.min(texture.width - 1, x));
      const clampedY = Math.max(0, Math.min(texture.height - 1, y));

      framed.frame = new Rectangle(
        clampedX,
        clampedY,
        Math.min(width, texture.frame.width - clampedX),
        Math.min(height, texture.frame.height - clampedY)
      );
    }
  }
  let tiles = storage.get<
    Array<{
      textureIndex: string;
      x: number;
      y: number;
      width: number;
      height: number;
    }>
  >("tiles", []);
  function onSave() {
    tiles = storage.get("tiles", []);
    tiles.push({ textureIndex: $page.params.index, x, y, width, height });
    storage.set("tiles", tiles);
  }
</script>

<svelte:head><title>{data.name}</title></svelte:head>
<a href="/editor">Terug</a>
<EditorPanel>
  <Engine slot="preview" backgroundColor={0x626262}>
    <Container>
      {#if texture && framed}
        <Sprite {texture} x={5} y={5} />
        <Sprite texture={framed} x={5} y={10 + texture.height} />
      {/if}
    </Container>
    <Container>
      <Control type="topleft" x={x + 4} y={y + 4} />
      <Control type="bottomright" x={x + width + 3} y={y + height + 3} />
    </Container>
  </Engine>

  <label>
    Naam
    <input type="text" bind:value={name} />
  </label>
  {#if framed}
    <label class:invalid={x < 0 || x > framed.frame.width}>
      X
      <input type="number" bind:value={x} />
    </label>
    <label>
      Y
      <input type="number" bind:value={y} />
    </label>
    <label class:invalid={width !== framed.frame.width}>
      Breedte
      <input type="number" bind:value={width} />
    </label>
    <label>
      Hoogte
      <input type="number" bind:value={height} />
    </label>
    <button on:click={onSave}>Save</button>
  {/if}
</EditorPanel>

<style lang="scss">
  label {
    display: block;
    &.invalid {
      color: #fb5b5b;
    }
  }
  input {
    display: block;
    width: 70px;
  }
</style>
