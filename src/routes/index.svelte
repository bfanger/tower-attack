<script lang="ts">
  import { Container } from "svelte-pixi";
  import Game from "$lib/components/Engine.svelte";
  import Land from "$lib/components/Land.svelte";
  import Base from "$lib/components/Base.svelte";
</script>

<Game>
  <Container>
    {#each { length: 12 } as _, y}
      {#each { length: 16 } as _, x}
        <Land {x} {y} />
      {/each}
    {/each}
  </Container>
  <Base x={40} y={20} good />

  <Base x={400} y={220} />
</Game>
