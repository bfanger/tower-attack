<script lang="ts">
  import { Rectangle } from "pixi.js";
  import { Sprite } from "svelte-pixi";
  import Texture from "./Texture.svelte";

  export let x: number;
  export let y: number;

  export let good = false;

  $: frame = good ? new Rectangle(4, 5, 13, 13) : new Rectangle(18, 5, 13, 13);
  const scale = 5;

  function toggle() {
    good = !good;
  }
</script>

<Texture resource="base" let:texture {frame}>
  <Sprite interactive {texture} {scale} {x} {y} on:click={toggle} />
</Texture>
