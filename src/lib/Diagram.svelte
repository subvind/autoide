<script lang="ts">
  import { Svelvet, Node, Anchor, Edge, Controls } from 'svelvet';

  export let width: number;
  export let height: number;
</script>

<Svelvet width={width} height={height - 300} theme="dark" initialZoom={0.6} minimap>
	<Node />
	<Node label="Demo Node" inputs={3} />
	<Node id="node-id" inputs={2} />
	<Node bgColor="red" inputs={10} outputs={5} height={200} position={{ x: 100, y: 100 }} />
	<Controls slot="controls" horizontal />
</Svelvet>
test