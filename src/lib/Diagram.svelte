<script lang="ts">
  import { Svelvet, Node, Anchor, Edge, Controls } from 'svelvet';

	import MyEdge from '../lib/Edge.svelte'

  export let width: number;
  export let height: number;

	const nodes: Array<any> = [
    {
      id: 1,
      positionX: 100,
			positionY: 300,
      data: { label: "Resize node" },
      dimensionWidth: 200,
      dimensionHeight: 200,
      bgColor: "yellow",
      textColor: "black",
			label: "FizzBuzz",
			borderColor: "black",
			inputAnchors: [],
			outputAnchors: [
				{
					id: 'out-fizz',
					connections: [['fizz', 'in-fizz']]
				},
				{
					id: 'out-buzz',
					connections: [['buzz', 'in-buzz']]
				}
			]
    },
    {
      id: 'fizz',
      positionX: 500,
			positionY: 100,
      data: { label: "Mixed Anchors" },
      dimensionWidth: 200,
      dimensionHeight: 200,
      bgColor: "red",
      textColor: "white",
			label: "Fizz",
			borderColor: "black",
			inputAnchors: [
				{
					id: 'in-fizz'
				},
			],
			outputAnchors: []
    },
    {
      id: 'buzz',
      positionX: 500,
			positionY: 500,
      data: { label: "Mixed Anchors" },
      dimensionWidth: 200,
      dimensionHeight: 200,
      bgColor: "blue",
      textColor: "white",
			label: "Buzz",
			borderColor: "black",
			inputAnchors: [
				{
					id: 'in-buzz'
				},
			],
			outputAnchors: []
    }
  ];
</script>

<Svelvet width={width} height={height} theme="dark" initialZoom={1} minimap nodeCreate={true}>
	{#each nodes as node}
		<Node 
			id={node.id} 
			bgColor={node.bgColor}
			textColor={node.textColor}
			height={node.dimensionHeight}
			width={node.dimensionWidth}
			position={{ x: node.positionX, y: node.positionY }}
			borderColor={node.borderColor}
			on:connection={() => {
				alert('node connected')
			}}
			on:disconnection={() => {
				alert('node disconnected')
			}}
		>

			<div style="width: 100%;">
				<div class="input-anchors">
					{#each node.inputAnchors as anchor}
						<Anchor id={anchor.id} edge={MyEdge} direction="west" connections={[]} output />
					{/each}
				</div>
				<h1>{node.label}</h1>	
				<div class="output-anchors">
					{#each node.outputAnchors as anchor}
						<Anchor id={anchor.id} edge={MyEdge} direction="east" connections={anchor.connections} output />
					{/each}
				</div>
			</div>
		</Node>
	{/each}

</Svelvet>

<style>
	.input-anchors {
		float: left;
	}
	.output-anchors {
		position: fixed;
		right: -5px;
	}

	:global(.output-anchors .anchor-wrapper) {
		margin-top: 5px;
		margin-bottom: 5px;
	}
</style>