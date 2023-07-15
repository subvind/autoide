<script lang="ts">
  import Greet from '../lib/Greet.svelte'
  import Diagram from '../lib/Diagram.svelte'

  let height: number = 0;
  let width: number = 0;
</script>

<svelte:window bind:innerHeight={height} bind:innerWidth={width} />

<Diagram height={height} {width} />

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentations</p>
<Greet />
