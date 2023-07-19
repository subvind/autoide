<script lang="ts">
  import { Edge } from 'svelvet';

  function destroy() {

  }
</script>

<Edge let:path let:destroy edgeClick="{() => alert('Message data travels from sh to output.')}" step color="#111">
  <path d={path} />
  <button on:click={destroy} slot="label" style="">
    <p style="padding: 0; margin: 0;">sh to output</p>
  </button>
</Edge>

<style>
	path {
		stroke: purple;
		stroke-width: 4px;
	}
</style>