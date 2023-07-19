<script lang="ts">
  import { Svelvet, Node, Anchor, Edge, Controls } from 'svelvet';

	import DataToJson from './edges/data-to-json.svelte'
	import DataToXml from './edges/data-to-xml.svelte'
	import ShToOutput from './edges/sh-to-output.svelte'
	import Code from '../lib/Code.svelte'

  export let width: number;
  export let height: number;

	const nodes: Array<any> = [
    {
      id: 1,
      positionX: 100,
			positionY: 300,
      data: { label: "Resize node" },
      dimensionWidth: 400,
      dimensionHeight: 25,
      bgColor: "black",
      textColor: "white",
			label: "FizzBuzz",
			borderColor: "black",
			rows: [
				{
					inputAnchor: null,
					value: `function main () {\n  return { hello: "world" };\n}`,
					language: "typescript",
					outputAnchor: {
						id: 'out-fizzbuzz-a',
						connections: [['fizz', 'in-fizz-a']]
					}
				},
				{
					inputAnchor: null,
					value: `inom hello world --key="value"`,
					language: "sh",
					outputAnchor: {
						id: 'out-fizzbuzz-b',
						connections: [['fizz', 'in-fizz-b']]
					}
				},
				{
					inputAnchor: null,
					value: `function main (A) {\n  return A.dataToJson();\n}`,
					language: "typescript",
					outputAnchor: {
						id: 'out-fizzbuzz-c',
						connections: [['buzz', 'in-buzz-c']]
					}
				},
				{
					inputAnchor: null,
					value: "hello world",
					language: "text",
					outputAnchor: null
				},
				{
					inputAnchor: null,
					value: `function main (D) {\n  return D.textToString();\n}`,
					language: "typescript",
					outputAnchor: null
				},
			]
    },
    {
      id: 'fizz',
      positionX: 700,
			positionY: 100,
      data: { label: "Mixed Anchors" },
      dimensionWidth: 400,
      dimensionHeight: 25,
      bgColor: "black",
      textColor: "white",
			label: "Fizz",
			borderColor: "black",
			rows: [
				{
					inputAnchor: {
						id: 'in-fizz-a'
					},
					value: `{ "hello": "world" }`,
					language: "json",
					outputAnchor: null
				},
				{
					inputAnchor: {
						id: 'in-fizz-b'
					},
					value: "hello world",
					language: "sh",
					outputAnchor: null
				},
			]
    },
    {
      id: 'buzz',
      positionX: 700,
			positionY: 500,
      data: { label: "Mixed Anchors" },
      dimensionWidth: 400,
      dimensionHeight: 25,
      bgColor: "black",
      textColor: "white",
			label: "Buzz",
			borderColor: "black",
			rows: [
				{
					inputAnchor: null,
					value: `<div test="true">\n  hello world\n</div>`,
					language: "xml",
					outputAnchor: null
				},
				{
					inputAnchor: {
						id: 'in-buzz-b'
					},
					value: "hello world",
					language: "sh",
					outputAnchor: null
				},
				{
					inputAnchor: {
						id: 'in-buzz-c'
					},
					value: `{ "hello": "world" }`,
					language: "json",
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
			on:duplicate={() => {
				alert('node duplicated')
			}}
		>
			<div class="table">
				<h1 class="header">
					{node.label} 
					<span style="float: right;">config / code</span>
				</h1>
				{#each node.rows as row}
					<div class="row">
						<div class="input-anchors">
							{#if row.inputAnchor !== null}
								<Anchor id={row.inputAnchor.id} direction="west" connections={[]} output />
							{/if}
						</div>
						<Code value={row.value} language={row.language} />
						<div class="output-anchors">
							{#if row.outputAnchor !== null}
								{#if row.language === 'xml'}
									<Anchor id={row.outputAnchor.id} edge={DataToXml} direction="east" connections={row.outputAnchor.connections} output />
								{:else if row.language === 'typescript'}
									<Anchor id={row.outputAnchor.id} edge={DataToJson} direction="east" connections={row.outputAnchor.connections} output />
								{:else if row.language === 'javascript'}
									<Anchor id={row.outputAnchor.id} edge={DataToJson} direction="east" connections={row.outputAnchor.connections} output />
								{:else if row.language === 'sh'}
									<Anchor id={row.outputAnchor.id} edge={ShToOutput} direction="east" connections={row.outputAnchor.connections} output />
								{/if}
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
		min-height: 30px;
		background: #202020;
		border-bottom: 1px solid #333;
		border-top: 1px solid #000;
		align-items: center;
		display: flex;
	}

	.table .header {
		margin: 0;
		padding: 0.5em;
		background: #777;
		color: #111;
		font-weight: 100;
	}

	.input-anchors {
		position: fixed;
		left: -18px;
	}
	.output-anchors {
		position: fixed;
		right: -18px;
	}

	:global(.output-anchors .anchor-wrapper) {
		margin-top: 5px;
		margin-bottom: 5px;
	}

	:global(.svelvet-node) {
		align-items: start !important;
	}
</style>