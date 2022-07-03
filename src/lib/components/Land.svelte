<script lang="ts">
  import { Rectangle } from "pixi.js";
  import { Sprite } from "svelte-pixi";
  import Texture from "./Texture.svelte";

  export let x: number;
  export let y: number;

  let frame = new Rectangle(0, 0, 6, 6);

  function reframe() {
    const tileX = Math.floor(Math.random() * 3);
    const tileY = Math.floor(Math.random() * 4);
    frame = new Rectangle(tileX * 7, tileY * 7, 6, 6);
  }
  reframe();
  const size = 6;
  const scale = 5;
</script>

<Texture resource="land" let:texture {frame}>
  <Sprite
    interactive
    {texture}
    {scale}
    x={x * size * scale}
    y={y * size * scale}
    on:click={() => reframe()}
  />
</Texture>
