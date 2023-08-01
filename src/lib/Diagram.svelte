<script lang="ts">
  import { Svelvet, Node, Anchor, Edge, Controls } from 'svelvet';

	import DataToJson from './edges/data-to-json.svelte'
	import DataToXml from './edges/data-to-xml.svelte'
	import ShToOutput from './edges/sh-to-output.svelte'
	import RunCode from './edges/run-code.svelte'
	import Code from '../lib/Code.svelte'

  export let width: number;
  export let height: number;

	const exampleFlow = `<file id="A" lang="typescript">
	<inputs>
		<anchor node="fizz" file="A"></anchor>
	</inputs>
	<outputs>
		<anchor node="fizz" file="A"></anchor>
	</outputs>
</file>`

	const demoMain = `let event = "customer:created";
let data = undefined; // { hello: "world" };

function main (fizzbuzz, fizz, buzz) {
  let report = [];
  for (let i = 0; i < 100; i++) {
    if (i%15) {
      report.push(fizzbuzz(data));
    } else if (i%3) {
      report.push(fizz(data));
    } else if (i%5) {
      report.push(buzz(data));
    }
  }
  console.log(report);
}`

	const exampleMain = `let event = "product:order_placed";
let data = undefined; // { hello: "world" };

function main (fizzbuzz, fizz, buzz) {
  setInterval(() => {
    console.log(fizzbuzz(data));
    console.log(fizz(data), buzz(data));
  }, 1000);
}`

	const nodes: Array<any> = [
    {
      id: 'product:order_placed',
			kind: 'main',
      positionX: 800,
			positionY: -500,
      dimensionWidth: 475,
      dimensionHeight: 25,
      bgColor: "black",
      textColor: "white",
			borderColor: "black",
			active: 'nodes',
			files: [
				{
					inputAnchor: null,
					value: exampleMain,
					language: "typescript",
					outputAnchor: null
				},
				{
					inputAnchor: null,
					value: `function fizzbuzz (req, res) {\n  return res.D.textToString();\n}`,
					language: "typescript",
					outputAnchor: {
						id: 'out-example-a',
						connections: [['fizzbuzz', 'link-fizzbuzz']]
					}
				},
				{
					inputAnchor: null,
					value: `function fizz (req, res) {\n  return res.B.textToString();\n}`,
					language: "typescript",
					outputAnchor: {
						id: 'out-example-b',
						connections: [['fizz', 'link-fizz']]
					}
				},
				{
					inputAnchor: null,
					value: `function buzz (req, res) {\n  return res.C.textToString();\n}`,
					language: "typescript",
					outputAnchor: {
						id: 'out-example-c',
						connections: [['buzz', 'link-buzz']]
					}
				},
			]
		},
    {
      id: 'customer:created',
			kind: 'main',
      positionX: 100,
			positionY: -300,
      dimensionWidth: 475,
      dimensionHeight: 25,
      bgColor: "black",
      textColor: "white",
			borderColor: "black",
			active: 'nodes',
			files: [
				{
					inputAnchor: null,
					value: demoMain,
					language: "typescript",
					outputAnchor: null
				},
				{
					inputAnchor: null,
					value: `function fizzbuzz (req, res) {\n  return res.F.textToString();\n}`,
					language: "typescript",
					outputAnchor: {
						id: 'out-demo-a',
						connections: [['fizzbuzz', 'link-fizzbuzz']]
					}
				},
				{
					inputAnchor: null,
					value: `function fizz (req, res) {\n  return res.C.textToString();\n}`,
					language: "typescript",
					outputAnchor: {
						id: 'out-demo-b',
						connections: [['fizz', 'link-fizz']]
					}
				},
				{
					inputAnchor: null,
					value: `function buzz (req, res) {\n  return res.D.textToString();\n}`,
					language: "typescript",
					outputAnchor: {
						id: 'out-demo-c',
						connections: [['buzz', 'link-buzz']]
					}
				},
			]
		},
    {
      id: 'fizzbuzz',
			kind: 'block',
      positionX: 100,
			positionY: 300,
      dimensionWidth: 475,
      dimensionHeight: 25,
      bgColor: "black",
      textColor: "white",
			borderColor: "black",
			active: 'files',
			files: [
				{
					inputAnchor: null,
					value: `function run () {\n  return req;\n}`,
					language: "typescript",
					flow: exampleFlow,
					outputAnchor: {
						id: 'out-fizzbuzz-a',
						connections: [['fizz', 'in-fizz-a']]
					}
				},
				{
					inputAnchor: null,
					value: `inom console --log="hello world"`,
					language: "sh",
					flow: ``,
					outputAnchor: {
						id: 'out-fizzbuzz-b',
						connections: [['fizz', 'in-fizz-b']]
					}
				},
				{
					inputAnchor: null,
					value: `function run (A) {\n  return A.dataToJson();\n}`,
					language: "typescript",
					flow: ``,
					outputAnchor: {
						id: 'out-fizzbuzz-c',
						connections: [['buzz', 'in-buzz-c']]
					}
				},
				{
					inputAnchor: null,
					value: "hello world",
					language: "text",
					flow: ``,
					outputAnchor: null
				},
				{
					inputAnchor: null,
					value: `function run (C) {\n  return C.dataToJson();\n}`,
					language: "typescript",
					flow: ``,
					outputAnchor: {
						id: 'out-fizzbuzz-e',
						connections: [['buzz', 'in-buzz-b']]
					}
				},
				{
					inputAnchor: null,
					value: `fizzbuzz`,
					language: "text",
					flow: ``,
					outputAnchor: null
				},
			],
			moduleAnchor: {
				id: 'link-fizzbuzz',
				connections: [['main', 'in-main-a']]
			}
    },
    {
      id: 'fizz',
			kind: 'block',
      positionX: 800,
			positionY: 100,
      dimensionWidth: 475,
      dimensionHeight: 25,
      bgColor: "black",
      textColor: "white",
			borderColor: "black",
			active: 'files',
			files: [
				{
					inputAnchor: {
						id: 'in-fizz-a'
					},
					value: `{ "hello": "world" }`,
					language: "json",
					flow: ``,
					outputAnchor: null
				},
				{
					inputAnchor: {
						id: 'in-fizz-b'
					},
					value: "hello world",
					language: "sh",
					flow: ``,
					outputAnchor: null
				},
				{
					inputAnchor: null,
					value: "fizz",
					language: "text",
					flow: ``,
					outputAnchor: null
				},
			],
			moduleAnchor: {
				id: 'link-fizz',
				connections: [['main', 'in-main-b']]
			}
    },
    {
      id: 'buzz',
			kind: 'block',
      positionX: 800,
			positionY: 500,
      dimensionWidth: 475,
      dimensionHeight: 25,
      bgColor: "black",
      textColor: "white",
			borderColor: "black",
			active: 'files',
			files: [
				{
					inputAnchor: null,
					value: `<div test="true">\n  hello world\n</div>`,
					language: "xml",
					flow: ``,
					outputAnchor: null
				},
				{
					inputAnchor: {
						id: 'in-buzz-c'
					},
					value: `{ "hello": "world" }`,
					language: "json",
					flow: ``,
					outputAnchor: null
				},
				{
					inputAnchor: {
						id: 'in-buzz-b'
					},
					value: "hello world",
					language: "sh",
					flow: ``,
					outputAnchor: null
				},
				{
					inputAnchor: null,
					value: "buzz",
					language: "text",
					flow: ``,
					outputAnchor: null
				},
			],
			moduleAnchor: {
				id: 'link-buzz',
				connections: [['main', 'in-main-c']]
			}
    }
  ];
</script>

<Svelvet width={width} height={height} theme="dark" translation={{ x: -50, y: 550 }} initialZoom={1} minimap nodeCreate={true} trackpadPan={true}>
	<!-- nodes -->
	<!-- nodes -->
	<!-- nodes -->
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
				{#if node.kind !== 'main'}
					<div class="config">
						<div style="flex: 1;"></div>
						<Anchor id={node.moduleAnchor.id} direction="north" connections={[]} output />
						<div style="flex: 1;"></div>
					</div>
				{/if}
				<div class="switch">

					{#if node.kind === 'main'}
						<button on:click={() => {node.active = 'nodes'}} class={node.active === 'nodes' ? 'selected' : ''}>nodes</button>
						<button on:click={() => {node.active = 'order'}} class={node.active === 'order' ? 'selected' : ''}>order</button>
					{:else if node.kind === 'block'}
						<button on:click={() => {node.active = 'files'}} class={node.active === 'files' ? 'selected' : ''}>files</button>
						<button on:click={() => {node.active = 'flow'}} class={node.active === 'flow' ? 'selected' : ''}>flow</button>
						<button on:click={() => {node.active = 'imports'}} class={node.active === 'imports' ? 'selected' : ''}>imports</button>
						<button on:click={() => {node.active = 'order'}} class={node.active === 'order' ? 'selected' : ''}>order</button>
					{/if}
				</div>
				<h1 class="header">
					{#if node.kind === 'main'}
						[{node.id}]
					{:else if node.kind === 'block'}
						&#123;{node.id}&#125;
					{/if}
				</h1>
				{#each node.files as file}
					<div class="file">
						<div class="input-anchors">
							{#if file.inputAnchor !== null}
								<Anchor id={file.inputAnchor.id} direction="west" connections={[]} output />
							{/if}
						</div>
						<Code active={node.active} flow={file.flow} value={file.value} language={file.language} />
						<div class="output-anchors">
							{#if file.outputAnchor !== null}
								{#if node.kind === 'main'}
									<Anchor id={file.outputAnchor.id} edge={RunCode} direction="east" connections={file.outputAnchor.connections} output />
								{:else if file.language === 'xml'}
									<Anchor id={file.outputAnchor.id} edge={DataToXml} direction="east" connections={file.outputAnchor.connections} output />
								{:else if file.language === 'typescript'}
									<Anchor id={file.outputAnchor.id} edge={DataToJson} direction="east" connections={file.outputAnchor.connections} output />
								{:else if file.language === 'javascript'}
									<Anchor id={file.outputAnchor.id} edge={DataToJson} direction="east" connections={file.outputAnchor.connections} output />
								{:else if file.language === 'sh'}
									<Anchor id={file.outputAnchor.id} edge={ShToOutput} direction="east" connections={file.outputAnchor.connections} output />
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

	.table .file {
		min-height: 20px;
		padding: 0.5em 0;
		background: #202020;
		border-bottom: 1px solid #333;
		border-top: 1px solid #000;
		align-items: center;
		display: flex;
	}

	.table .switch {
		float: right; 
		padding: 0.5em;
	}

	.table .switch button {
		background: #111;
		color: #fff;
		border: 1px solid #000;
	}
	
	.table .switch .selected {
		background: #fff;
		color: #111;
		border: none;
	}

	.table .header {
		margin: 0;
		padding: 0.5em;
		background: #777;
		color: #111;
		font-weight: 100;
	}

	.table .config {
		width: 100%;
		display: flex;
		height: 0;
		position: relative;
		top: -18px;
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