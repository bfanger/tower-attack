<script lang="ts">
  import { Rectangle } from "pixi.js";
  import { Sprite } from "svelte-pixi";
  import Texture from "./Texture.svelte";

  export let x: number;
  export let y: number;

  const size = 6;
  let frame = new Rectangle(0, 0, size, size);

  function reframe() {
    const tileX = Math.floor(Math.random() * 3);
    const tileY = Math.floor(Math.random() * 4);
    frame = new Rectangle(tileX * (size + 1), tileY * (size + 1), 6, 6);
  }
  reframe();
</script>

<Texture src="land.png" let:texture {frame}>
  <Sprite
    interactive
    {texture}
    x={x * size}
    y={y * size}
    on:click={() => reframe()}
  />
</Texture>
