<script lang="ts">
  import { Texture, Rectangle, Loader, LoaderResource } from "pixi.js";

  export let resource: string;
  export let frame: Rectangle;

  let texture: Texture;
  $: onResource(Loader.shared.resources[resource]);

  function onResource(loaded: LoaderResource | undefined) {
    if (loaded?.texture) {
      texture = new Texture(loaded.texture.baseTexture, frame);
    } else {
      console.warn("Missing resource", resource);
    }
  }
  $: if (texture) {
    texture.frame = frame;
  }
</script>

{#if texture}
  <slot {texture} />
{/if}
