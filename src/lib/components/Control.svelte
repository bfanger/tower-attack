<script lang="ts">
  import { Rectangle, Texture } from "pixi.js";
  import { Sprite } from "svelte-pixi";

  export let x: number;
  export let y: number;
  export let type: keyof typeof map;

  let texture: Texture | undefined;
  const map = {
    topleft: new Rectangle(0, 0, 3, 3),
    bottomright: new Rectangle(3, 0, 3, 3),
  };
  Texture.fromURL("/assets/editor.png").then((result) => {
    texture = new Texture(result.baseTexture, map[type]);
  });
</script>

{#if texture}
  <Sprite {texture} {x} {y} />
{/if}
