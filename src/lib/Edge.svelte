<script lang="ts">
  import { Edge } from 'svelvet';

  function destroy() {

  }
</script>

<Edge let:path let:destroy edgeClick="{() => alert('Edge clicked')}" step color="#111">
  <path d={path} />
  <button on:click={destroy} slot="label">
    <p>Custom Label</p>
  </button>
</Edge>

<style>
	path {
		stroke: green;
		stroke-width: 4px;
	}
</style>