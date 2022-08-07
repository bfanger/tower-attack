<script lang="ts" context="module">
  const promises = new Map<string, Promise<Texture>>();
</script>

<script lang="ts">
  import { Texture, Rectangle } from "pixi.js";

  export let src: string;
  export let frame: Rectangle;

  let texture: Texture;

  $: load(`assets/${src}`);

  function load(url: string) {
    const promise = promises.get(url) || Texture.fromURL(url);
    promises.set(url, promise);
    promise.then((loaded) => {
      texture = new Texture(loaded.baseTexture, frame);
    });
  }

  // $: onResource(Loader.shared.resources[resource]);

  // function onResource(loaded: LoaderResource | undefined) {
  //   if (loaded?.texture) {
  //     texture = new Texture(loaded.texture.baseTexture, frame);
  //   } else {
  //     console.warn("Missing resource", resource);
  //   }
  // }
  $: if (texture) {
    texture.frame = frame;
  }
</script>

{#if texture}
  <slot {texture} />
{/if}
