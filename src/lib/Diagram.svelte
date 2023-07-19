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
      dimensionHeight: 25,
      bgColor: "black",
      textColor: "white",
			label: "FizzBuzz",
			borderColor: "black",
			rows: [
				{
					inputAnchor: null,
					outputAnchor: null
				},
				{
					inputAnchor: null,
					outputAnchor: {
						id: 'out-fizz',
						connections: [['fizz', 'in-fizz']]
					}
				},
				{
					inputAnchor: null,
					outputAnchor: {
						id: 'out-buzz',
						connections: [['buzz', 'in-buzz']]
					}
				},
				{
					inputAnchor: null,
					outputAnchor: null
				},
				{
					inputAnchor: null,
					outputAnchor: null
				},
			]
    },
    {
      id: 'fizz',
      positionX: 500,
			positionY: 100,
      data: { label: "Mixed Anchors" },
      dimensionWidth: 200,
      dimensionHeight: 25,
      bgColor: "black",
      textColor: "white",
			label: "Fizz",
			borderColor: "black",
			rows: [
				{
					inputAnchor: null,
					outputAnchor: null
				},
				{
					inputAnchor: {
						id: 'in-fizz'
					},
					outputAnchor: null
				},
			]
    },
    {
      id: 'buzz',
      positionX: 500,
			positionY: 500,
      data: { label: "Mixed Anchors" },
      dimensionWidth: 200,
      dimensionHeight: 25,
      bgColor: "black",
      textColor: "white",
			label: "Buzz",
			borderColor: "black",
			rows: [
				{
					inputAnchor: null,
					outputAnchor: null
				},
				{
					inputAnchor: {
						id: 'in-buzz'
					},
					outputAnchor: null
				},
				{
					inputAnchor: null,
					outputAnchor: null
				},
			]
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
			<div class="table">
				<h1 class="header">{node.label}</h1>
				{#each node.rows as row}
					<div class="row">
						<div class="input-anchors">
							{#if row.inputAnchor !== null}
								<Anchor id={row.inputAnchor.id} edge={MyEdge} direction="west" connections={[]} output />
							{/if}
						</div>
						<div class="output-anchors">
							{#if row.outputAnchor !== null}
								<Anchor id={row.outputAnchor.id} edge={MyEdge} direction="east" connections={row.outputAnchor.connections} output />
							{/if}
						</div>
					</div>
				{/each}
			</div>
		</Node>
	{/each}

</Svelvet>

<style>
	.table {
		width: 100%;
		border: 1px solid #000;
	}

	.table .row {
		height: 50px;
		background: #ccc;
		border-bottom: 1px solid #777;
		align-items: center;
		display: flex;
	}

	.table .header {
		margin: 0;
		padding: 0.5em;
		background: #777;
		color: #111;
		font-weight: 100;
		border-bottom: 1px solid #000;

	}

	.input-anchors {
		position: fixed;
		left: -5px;
	}
	.output-anchors {
		position: fixed;
		right: -5px;
	}

	:global(.output-anchors .anchor-wrapper) {
		margin-top: 5px;
		margin-bottom: 5px;
	}

	:global(.svelvet-node) {
		align-items: start !important;
	}
</style>