<script lang="ts">
  import { Edge } from 'svelvet';

  function destroy() {

  }
</script>

<Edge let:path let:destroy edgeClick="{() => alert('Message data travels from data to xml.')}" step color="#111">
  <path d={path} />
  <button on:click={destroy} slot="label" style="">
    <p style="padding: 0; margin: 0;">data to xml</p>
  </button>
</Edge>

<style>
	path {
		stroke: green;
		stroke-width: 4px;
	}
</style>