<script lang="ts">
  import { Loader, SCALE_MODES } from "pixi.js";

  import { Application, Text } from "svelte-pixi";

  Loader.shared.baseUrl = "/assets/";

  let loading = true;
  Loader.shared.add("land", "land.png");
  Loader.shared.add("base", "base.png");

  Loader.shared.load(({ resources }) => {
    for (const resource of Object.values(resources)) {
      if (resource.texture?.baseTexture) {
        resource.texture.baseTexture.scaleMode = SCALE_MODES.NEAREST;
      }
    }

    loading = false;
  });
</script>

<Application width={30 * 16} height={30 * 12} backgroundColor={0xff6b00}>
  {#if loading}
    <Text text="Loading..." />
  {:else}
    <slot />
  {/if}
</Application>

<style lang="scss">
  :global {
    @import "../global.scss";
    canvas {
      width: 100% !important;
      height: auto !important;
      image-rendering: pixelated;
    }
  }
</style>
