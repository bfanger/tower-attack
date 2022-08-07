<script lang="ts" context="module">
  // export type ResourceType = "land" | "base";
</script>

<script lang="ts">
  import { Application } from "svelte-pixi";

  export let backgroundColor = 0x271102;
</script>

<Application width={10 * 16} height={10 * 12} {backgroundColor}>
  <slot />
</Application>

<style lang="scss">
  :global {
    canvas {
      width: 100% !important;
      height: auto !important;
      image-rendering: pixelated;
    }
  }
</style>
