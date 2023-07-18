<script lang="ts">
  import Diagram from '../lib/Diagram.svelte'

  let height: number = 0;
  let width: number = 0;
</script>

<svelte:window bind:innerHeight={height} bind:innerWidth={width} />

<Diagram height={height} {width} />
