<script lang="ts">
  import { Edge } from 'svelvet';

  function destroy() {

  }
</script>

<Edge let:path let:destroy edgeClick="{() => alert('The following module gets run file by file.')}" color="#111">
  <path d={path} />
  <button on:click={destroy} slot="label" style="background: #000; border: 0;">
    <p style="padding: 0; margin: 0; color: #aaa;">run code</p>
  </button>
</Edge>

<style>
	path {
		stroke: orange;
		stroke-width: 4px;
	}
</style>